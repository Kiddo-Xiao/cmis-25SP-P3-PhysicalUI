# CMIS P3-PhysicalUI: Handheld Bow and Arrow

Tutorial By Flora

## Project Overview

This project consists of a physics-based optimization system for bow toy designs with a graphical user interface. The application allows users to:

- Select different user profiles (Child, Adult, Professional)
- Customize bow parameters (thickness, curvature, stiffness, grip width)
- Optimize design based on user profiles and preferences
- Simulate performance metrics (launch speed, draw force, accuracy)
- Export the final model as an STL file for 3D printing

## Files Structure

- **BowArrowOpt.py** - Core optimization engine and physics calculations
- **BowArrowUI.py** - PyQt5-based graphical user interface

## For Team Members

### Getting Started

1. You don't need to modify **BowArrowUI.py** - the UI is already complete
![alt text](image.png)
2. Focus your attention on **BowArrowOpt.py** where the physics and optimization logic lives
3. Look for `TODO:` comments in BowArrowOpt.py for areas that need improvement

### TODO Items for Implementation

I've marked several areas in BowArrowOpt.py that could use your expertise:

1. **Improve launch speed estimation** - The current physics model is simplified
2. **Enhance draw force calculation** - Needs more accurate physics modeling
3. **Verify optimization method** - Review and enhance the current approach
4. **Update arrow parameter calculations** - Automatic arrow sizing based on bow parameters
5. **Improve performance score calculations** - More realistic performance metrics
6. **Add 3D printing parameter optimization** - Implement the print settings function

### Required Dependencies

- PyQt5
- NumPy
- trimesh
- SciPy
- pyqtgraph

### How to Run

```bash
# Create or Activate your own conda environment
# conda create -n name_of_your_own_env python=3.9 -y
conda activate name_of_your_own_env

# Install dependencies
pip install -r requirements.txt

# Run the application
python BowArrowUI.py
```

Make sure to place an STL model file in the `models` directory for the application to load. You can modify it at in the final part `main()` of `BowArrowUI.py`. Now I'm using `Bow_Arrow_Combined.stl` which includes both bow and arrow (maybe we need to print them saperately later).

## Key Features

- **User Profile Selection**: Customize for different users (children, adults, professionals)
- **Parameter Customization**: Adjust bow thickness, curvature, limb stiffness, and grip width
- **Palm Size Adaptation**: Automatically adjusts grip for different hand sizes
- **Optimization Algorithm**: Uses L-BFGS-B method to find optimal parameters
- **Performance Simulation**: Calculates key metrics like launch speed and accuracy
- **3D Visualization**: Real-time view of the bow model with parameter changes
- **STL Export**: Export models for 3D printing

## Physics Model

The system uses a simplified physics model to calculate:
- Arrow launch speed based on bow parameters
- Draw force required to use the bow
- Flight distance estimation
- Safety scores appropriate for different user groups

