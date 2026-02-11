# sonic_optic_display
A Sonic Optical Display

## Description
Sonic sensor/directional mic mapped to optical display with dot density for conveying sonic phenomenon visually.

Mapping microphone data -> visual space; determination of Direction of Arrival (DOA).

## Tools
- ODAS (Open embeddeD Audition System): Best for: Real-time, embedded, or low-latency applications (written in C). Function: It handles sound source localization, tracking, and separation. It works with arbitrary microphone geometries (circular, linear, etc.). Mapping: It outputs coordinates (azimuth/elevation) that you can easily transform into pixel coordinates for your optical display.

- Acoular: Post-processing and scientific analysis (Python-based). Function: Specifically designed for "acoustic photography." It includes advanced algorithms like Beamforming and CLEAN-SC to generate high-resolution "heat maps" of sound.

## Optical Integration Workflow

- Mapping directional audio to a camera lens/optical surface may require a Coordinate Transformation process.

### Tool / Method	Description
- Calibration	OpenCV Calibrate your camera to find its intrinsic parameters (FOV, focal length). This ensures the "point" the mic sees aligns with the "point" the lens sees.

- Data Sync	ODAS Studio:	An Electron-based GUI that provides a 3D visualizer for ODAS data. You can use its source code as a template for your own overlaid system.

- Mapping	Pyroomacoustics.	A Python library helpful for simulating the room geometry to ensure your mic array's "sweet spot" overlaps with the camera's FOV.

## Design Workflow
### Acoustic camera design

- Hardware Layout: Design your mic array (e.g., a 16-mic circular array) using KiCAD (Open-source PCB design).
- Processing: Use ODAS on a Raspberry Pi or PC to get real-time source coordinates.
- Visual Overlay: Use Python + OpenCV to grab the image feed. Convert the ODAS Spherical coordinates (Azimuth θ, Elevation ϕ) into Image Plane coordinates (x,y) using a perspective projection matrix.
- Draw a "Heat Map" or a "Target Reticle" over the video frames using a library like Matplotlib or OpenCV’s drawing functions.

## Visualization Concepts/Algorithms Notes:

For high-resolution results, focus on SRP-PHAT (Steered Response Power with Phase Transform). It is the industry-standard algorithm for localizing wideband signals like speech or machinery noise in real-time.
