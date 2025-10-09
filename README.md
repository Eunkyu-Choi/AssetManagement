# AssetManagement

Current version tests handling mutiple assets with different hierarchy levels and basic combat mechanics between groups.

[Tests conducted in this version]

Creating and destroying assets is working.
Adding and removing assets is working.
Moving assets to another asset is working.
Combat calculation is working.
Win and lose states are working.
Group to attack first has 64~65 percent chance to win. If attacked first, chances are 35~36 percent.(100000 cycles tested)



[Feature Guide]

All assets will be identified using an unique ID.

ID rule:

1. Starting from 0, add 1 everytime a new asset is created.
2. If an asset is destroyed, its ID will be recycled to the next asset being created.

---

All assets will have a predefined hierarchy level when created.

Hierarchy rule:

1. Asset with a defined hierarchy level can contain other assets with a lower hierarchy level.
2. If an asset containing other assets gets destroyed, the assets it holds will be relocated to the parent asset of the destroyed asset.
3. Asset types are as follows: Node, Group, Unit.
4. Hierarchy management will be performed using two interfaces: IParent, IChild.

---

All assets can be relocated as long as they can be a child of another asset

Repositioning rule:

1. When relocating an asset, all the other assets under the original assets should be moved together, maintaining the same hierarchy form.
2. An asset cannot be a child of itself.
3. Circular referance should be avoided. (In this case, hierarchy level will indirectly solve the issue)

---

Asset cycle:

→ Create a lowest asset(Unit) in a designated node(ally occupied stronghold).

→ If there are multiple units on the node, they can be gathered to a group asset. It is also possible to assign a single unit to a group.

→ Group asset can be controlled to move to another node or fight enemies. Unit asset without a group will be considered unregistered to the system, and will not be allowed to be controlled.

→ If a group asset has been defeated, its units will be scattered around the conflict node, along with losing control of all the team members.

→ The survived personnel will go under a survival phase, where it will move on its own until it is rescued by another group. Once deserted, the personal will no longer show its stat ui and will be represented as signal lost.

---

Asset creation rule:

1. Creation of an asset will be presented as recruitment or detachment contract.
2. Creation process consumes progress points, which can be earned through defeating enemies or performing certain tasks.
3. When creating an asset, the stats of the asset such as its traits or skills can be modified by using more progress points.
4. Once the asset is created, it will be contained under the node the creation process was made.