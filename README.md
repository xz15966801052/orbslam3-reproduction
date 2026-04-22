# ORB-SLAM3 Baseline Reproduction (WSL2 Ubuntu 22.04)

This repository is based on the official ORB-SLAM3 project and configured to run successfully under **Windows + WSL2 + Ubuntu 22.04.5 LTS**.

## Environment

- Windows 11
- WSL2
- Ubuntu 22.04 LTS
- OpenGL via WSLg
- Pangolin rebuilt manually
- GCC / CMake

## Build Instructions

```bash
cd ~/ORB_SLAM3
chmod +x build.sh
./build.sh
```
## EuRoC Dataset Example

Download EuRoC dataset (e.g. MH_01_easy) and extract to:
```bash
~/datasets/mav0
```
## Run monocular baseline:
```bash
cd ~/ORB_SLAM3

./Examples/Monocular/mono_euroc \
./Vocabulary/ORBvoc.txt \
./Examples/Monocular/EuRoC.yaml \
~/datasets \
./Examples/Monocular/EuRoC_TimeStamps/MH01.txt
```
## Convert ORB-SLAM3 Timestamp to Seconds
```bash
awk 'NF>=8 {printf "%.9f %.9f %.9f %.9f %.9f %.9f %.9f %.9f\n", $1/1e9, $2, $3, $4, $5, $6, $7, $8}' CameraTrajectory.txt > CameraTrajectory_sec.txt
```
## Trajectory Visualization:
```bash
~/.local/bin/evo_traj tum CameraTrajectory.txt -p --plot_mode xyz
```
## Accuracy Evaluation (APE)
```bash
 ~/.local/bin/evo_ape euroc ~/datasets/mav0/state_groundtruth_estimate0/data.csv CameraTrajectory_sec.txt -as -p
```
