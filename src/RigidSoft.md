Bullet3 中刚体与软体的交互主要通过其 **软体动力学模块（Soft Body Dynamics）** 实现，该模块与刚体动力学模块紧密集成。以下是主要机制和技术要点：

---

### 1. **软体表示**
软体通常用 **质点-弹簧系统** 或 **有限元模型** 表示：
- **质点网格**：软体由网格顶点（质点）和连接边（弹簧/约束）构成。
- **物理属性**：每个质点具有质量、速度，弹簧具有刚度、阻尼等参数。

---

### 2. **交互基本原理**
刚体与软体的交互本质上是 **碰撞检测与响应** 在混合系统中的应用：

#### **a) 碰撞检测**
- **软体包围盒**：基于软体顶点动态更新 AABB 包围盒，进行粗检测。
- **顶点级检测**：将软体的每个顶点/面与刚体进行精确碰撞检测（如 GJK/EPA 或 Bullet 内置的凸包检测）。
- **双向交互**：
  - 软体顶点 vs 刚体形状（如球体、立方体等）。
  - 刚体也可检测与软体三角形面的碰撞。

#### **b) 碰撞响应**
- **冲量法**：碰撞时对软体质点和刚体施加相反的冲量，满足动量守恒。
- **约束求解**：将碰撞转化为位置或速度约束，通过求解器（如 PBD 或 impulse-based 方法）处理。
- **摩擦力与恢复系数**：为软体顶点设置摩擦和弹性参数，模拟真实交互。

---

### 3. **实现流程（Bullet 代码层面）**
以下是典型流程（以 `btSoftBody` 和 `btRigidBody` 为例）：

#### **步骤 1：创建软体并添加到世界**
```cpp
btSoftBodyWorldInfo worldInfo;
btSoftBody* softBody = btSoftBodyHelpers::CreateFromTriMesh(...);
btRigidBody* rigidBody = ...; // 创建刚体

btSoftRigidDynamicsWorld* world = new btSoftRigidDynamicsWorld(...);
world->addSoftBody(softBody);
world->addRigidBody(rigidBody);
```

#### **步骤 2：交互通过碰撞检测触发**
- Bullet 的 `btSoftRigidCollisionAlgorithm` 处理软体-刚体碰撞。
- 在 `btSoftBody::solveCollisions` 中更新顶点位置以响应碰撞。

#### **步骤 3：求解器迭代**
在 `btSoftRigidDynamicsWorld::stepSimulation` 中：
1. 检测所有碰撞（包括软体-刚体对）。
2. 通过 `btSoftBodySolver` 更新软体顶点位置。
3. 对刚体应用软体碰撞产生的力（或冲量）。
4. 迭代求解约束（如 LCP 或 PBD 步骤）。

---

### 4. **关键参数与调优**
- **软体顶点质量**：影响惯性响应。
- **弹簧刚度**：控制形变程度。
- **阻尼**：减少振荡。
- **碰撞余量（margin）**：防止穿透。
- **迭代次数**：越多越稳定，但性能越低。

---

### 5. **示例代码片段**
```cpp
// 创建软体（如布料的网格）
btSoftBody* cloth = btSoftBodyHelpers::CreatePatch(
    worldInfo, corner1, corner2, resolutionX, resolutionY, 0, true);

// 设置软体物理参数
cloth->m_cfg.kDP = 0.01; // 阻尼
cloth->m_cfg.kDF = 0.5;  // 摩擦
cloth->m_cfg.collisions |= btSoftBody::fCollision::SDF_RD; // 启用与刚体碰撞

// 将软体固定在某个位置（如悬挂布料）
cloth->appendAnchor(0, rigidBodyAnchor); // 将顶点0锚定到刚体
```

---

### 6. **注意事项**
- **性能开销**：软体-刚体交互计算量大，需控制网格分辨率。
- **稳定性**：软体易振荡，需适当调整阻尼和迭代次数。
- **穿透问题**：复杂形状可能需要更小的步长或 CCD（连续碰撞检测）。

---

### 参考资料
- **Bullet 源码**：`btSoftRigidDynamicsWorld.cpp`、`btSoftBody.cpp`。
- **官方示例**：`SoftDemo`（位于 Bullet 的示例目录）。
- **论文**：《Soft Body Dynamics in Bullet Physics》（Erwin Coumans，Bullet 作者）。

通过以上机制，Bullet3 能够实现逼真的刚软交互（如布料落在刚体上、软球撞击墙壁等）。