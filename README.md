<div align="center">
<img width="249" height="98" alt="image" src="https://github.com/user-attachments/assets/0a33b2b2-7267-4a89-959d-b901f545766c" />

# OrcaSlicer-FLN

**OrcaSlicer-FLN** is based on **OrcaSlicer 2.5.0**.

This version was created by reviewing and modifying OrcaSlicer's original organic/tree support algorithms, inherited from Bambu Studio. The goal is to better address the requirements of **high-precision FDM printing**, especially in hardware configurations that fall outside the typical range for which the original automatic behavior works best.

OrcaSlicer currently handles tree-support branch collision calculations automatically. For a wide range of printers and nozzle sizes, this works very well. However, some more unusual configurations may expose limitations in that automatic behavior.

A good example is the use of a **0.2 mm nozzle**. The increase in geometric precision can be very significant, but the support collision algorithm does not necessarily scale with that precision in the same way. OrcaSlicer-FLN was created to give the user more direct control over these parameters when working with high-detail prints.

## How does the original algorithm work?

In the original OrcaSlicer implementation, the collision distance between organic support branches and the model is closely related to extrusion and line-width parameters.

In practice, the support automatically moves closer to or farther away from the model according to the calculated wall and extrusion widths.

This automatic behavior is effective for most normal printing conditions, but it gives the user limited control when working at very small scales.

## What does OrcaSlicer-FLN change?

In OrcaSlicer-FLN, the **XY distance between organic supports and the model can optionally be configured directly by the user**.

Making this possible required several parts of the organic support logic to be reviewed and restructured so that support connections could still reach the model even when relatively large XY clearances were used.

In the FLN version, organic branches can also be reduced to **0.6 mm**, allowing them to travel through narrow gaps and more complex geometries.

The improved XY-distance behavior allows branches to approach the model only where contact is required, then move away more quickly from the supported surface. This greatly reduces the risk of the support becoming fused to nearby details while still preserving small support contact points.

## Advantages

- Organizes the support branches in a much cleaner and more controlled way.
- Greatly reduces the chance of the supports fusing with the model.
- Makes support removal significantly easier after printing.

## Disadvantages

- Increases slicing time by approximately **10–20%**.
- Increases the complexity and fragility of the branches, requiring them to be printed more slowly.

### Original OrcaSlicer

With the XY clearance required to prevent the support from fusing to the model, the original OrcaSlicer quickly reduces the number of organic support branches.
At this scale, increasing the XY distance causes many small branches to disappear, reducing support coverage exactly where the geometry is most delicate.

<img width="807" height="804" alt="image" src="https://github.com/user-attachments/assets/43d36606-a5e7-49d3-ac85-f4d4e1c543f5" />


### OrcaSlicer-FLN

The FLN version preserves the support branches even when using a larger XY clearance.
Instead of moving the entire branch closer to the model, only the support tips approach the required contact areas. The rest of the branch moves away from the surface more quickly.
This allows FLN to maintain support coverage on very small features while greatly reducing the risk of the support fusing to the printed part.

<img width="795" height="790" alt="image" src="https://github.com/user-attachments/assets/31ca1ace-292c-4614-83a0-1a8b1c3b3ec7" />

## General Summary

OrcaSlicer-FLN is not a magic solution, but an additional tool for users who are looking for greater precision.

How effective it can be ultimately depends on how much time and patience you are willing to invest in properly tuning its settings for your specific printer, nozzle, material, and model.

## Custom Design

OrcaSlicer-FLN has its own visual identity, making it easy to use alongside the original OrcaSlicer without causing confusion between the two applications.

<img width="1919" height="1042" alt="image" src="https://github.com/user-attachments/assets/4926ad9a-337e-4af5-9ce6-0abac6a4c20f" />

<br>

## Credits

OrcaSlicer-FLN is a modified version of **OrcaSlicer 2.5.0**.

OrcaSlicer is an open-source project developed by **SoftFever and the OrcaSlicer community**, and is itself based on work from Bambu Studio, PrusaSlicer, Slic3r, SuperSlicer, and other open-source projects.

OrcaSlicer-FLN modifies parts of the original OrcaSlicer codebase, primarily focusing on organic/tree support behavior for high-precision FDM printing.

Original OrcaSlicer project:
https://github.com/OrcaSlicer/OrcaSlicer

## License

OrcaSlicer-FLN is distributed under the **GNU Affero General Public License v3.0 (AGPL-3.0)**, following the license of the original OrcaSlicer project.

This project contains modifications to OrcaSlicer 2.5.0.
