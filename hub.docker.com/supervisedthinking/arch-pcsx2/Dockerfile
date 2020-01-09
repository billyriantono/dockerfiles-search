########################################################################################################
# 
# Dockerfile for PCSX2
# 
########################################################################################################

FROM supervisedthinking/arch-base:latest

MAINTAINER Frank Hartung (supervisedthinking (@) gmail.com)

# Install PCSX2 & additional dependencies
RUN pacman -Sy --noconfirm pcsx2-git lib32-libglvnd nvidia lib32-nvidia-utils ttf-dejavu mesa-demos

# Remove downloaded packages & clean cache
RUN pacman -Scc --noconfirm
