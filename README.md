# Project EVOLVE v0.3.4

Paper 1.21.1 / Java 21 prototype.

## v0.3.4 - Control-safe Monster TPS prototype

The ProtocolLib CAMERA-packet implementation from v0.3.2-v0.3.3 has been removed. On a vanilla Java client, switching the camera to a separate entity prevents the normal Monster controller from behaving like a playable TPS character.

This version keeps the real player as the authoritative camera/controller so native WASD, mouse look, jump, sprint and left-click input remain available. The player is invisible, while the visible Monster body is rendered several blocks in front and slightly over-the-shoulder. This creates a TPS-like view without taking control away from the client.

### Changes
- ProtocolLib is no longer required.
- Removed `MonsterCameraController` and CAMERA packet usage.
- Monster body remains visible to its controller.
- Stage-specific visual body offsets under `monster.view`.
- Stage 1 default: forward 2.2 / side -0.65.
- Stage 2 default: forward 2.7 / side -0.85.
- Stage 3 default: forward 3.8 / side -1.25.
- Melee attack origin and target scan use the visible Monster body position.
- Corpse feeding distance uses the visible Monster body position.
- Existing wildlife, corpses, Evolution, attack effects and Stage changes remain enabled.

## Required server software
- Paper 1.21.1
- ProjectEVOLVE v0.3.4

ProtocolLib may remain installed for other plugins, but Project EVOLVE v0.3.4 does not depend on it.

## Test

```text
/evolve monster
/evolve wildlife 6
```

Check these points:
1. WASD movement works.
2. Mouse look works normally.
3. The Skeleton is visible in front/over-shoulder instead of covering the camera.
4. Left click shows `ATTACK! HIT xN` or `ATTACK! MISS`.
5. Attack particles originate from the visible Monster body area.

Then test:

```text
/evolve levelup
```

for Stage 2 and Stage 3 view offsets.

## Camera limitation
A true server-forced Java Edition F5 third-person camera while preserving normal movement/mouse input is not available through the ordinary Paper camera API. A true fixed TPS camera would require a client-side mod or a client feature specifically designed for custom cameras. This build therefore uses the server-safe visual-offset method for the vanilla client prototype.
