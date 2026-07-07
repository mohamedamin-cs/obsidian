**process vs physics_process** : 

| **Feature**     | **_process(delta)**                    | **_physics_process(delta)**             |
| --------------- | -------------------------------------- | --------------------------------------- |
| **Frequency**   | Every frame (Variable).                | Fixed interval (Default: 60 per sec).   |
| **Primary Use** | Visuals, UI, Input, Cameras.           | Movement, Collisions, Physics logic.    |
| **Delta Value** | Varies based on FPS.                   | Constant (e.g., $1/60 \approx 0.0166$). |
| **Sync**        | Synced to your monitor's Refresh Rate. | Synced to the Physics Engine.           |
