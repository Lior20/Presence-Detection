# ArduCAM Image Processing System

## Overview
This project implements an embedded image capture and processing system using ArduCAM with FreeRTOS. The system captures images through an OV2640 camera module, processes them in real-time, and can perform inference using a MobileNet model.

## Features
- Real-time image capture using OV2640 camera module
- Multi-threaded processing using FreeRTOS
- Support for both RAW and JPEG image formats
- Center crop functionality for image preprocessing
- RGB565 color format conversion
- MobileNet inference integration
- SPI and I2C communication interfaces
- UART debugging output

## Hardware Requirements
- Texas Instruments microcontroller (CC27XX series)
- ArduCAM with OV2640 sensor
- SPI and I2C interfaces
- UART interface for debugging

## Software Dependencies
- FreeRTOS
- TI-RTOS Drivers
  - GPIO
  - SPI
  - I2C
  - UART2
  - Power Management
- MobileNet inference library

## Project Structure
```
├── main_freertos.c      # Main application entry point and thread creation
├── spimaster.c          # SPI communication and thread implementation
├── ArduCAM.c           # Camera initialization and image capture functions
└── memorysaver.h       # Memory configuration for camera
```

## Key Components
1. **Thread Management**
   - SPI Thread: Handles image capture and data transfer
   - Inference Thread: Processes captured images
   - Thread synchronization using semaphores

2. **Camera Configuration**
   - Supports multiple image resolutions
   - Configurable image formats (RAW/JPEG)
   - Automatic file rotation
   - Customizable frame settings

3. **Image Processing Pipeline**
   - Center cropping
   - RGB565 conversion
   - MobileNet inference
   - Real-time processing

## Setup and Configuration

### Hardware Setup
1. Connect the ArduCAM to your TI microcontroller:
   - SPI pins for data transfer
   - I2C pins for camera control
   - CS pin for chip select
   - Power and ground connections

### Software Configuration
1. Configure the camera settings:
   ```c
   #define CENTER_CROP (1)
   #define RGB565_CONV (1)
   #define NUM_ROW     (240)
   #define NUM_COLS    (640)
   ```

2. Set up image processing parameters:
   ```c
   #define NUM_CROP_ROW (8)
   #define NUM_CROP_COL (96)
   #define EFF_COLS     (224)
   ```

## Usage

### Initialization
```c
// Initialize system components
Board_init();
GPIO_init();
SPI_init();
I2C_init();

// Initialize ArduCAM
Arducam_init();
```

### Image Capture
```c
// Start image capture
Arducam_start_capture();

// Wait for image ready
while (!Arducam_image_ready()) {
    // Wait for capture completion
}

// Read and process image
Arducam_read_image();
```

## Debug Output
The system provides debugging information through UART with a baud rate of 115200. This includes:
- Camera initialization status
- Image capture events
- Processing pipeline status
- Error messages

## Performance Considerations
- Image processing is performed in real-time
- Thread priorities are configured for optimal performance
- Memory management uses efficient buffer handling
- Power management features are implemented for better efficiency

## Troubleshooting

### Common Issues
1. SPI Communication Errors
   - Check CS pin configuration
   - Verify SPI clock rate
   - Ensure proper power supply

2. Camera Initialization Failures
   - Verify I2C connections
   - Check camera module compatibility
   - Confirm proper voltage levels

3. Image Quality Issues
   - Adjust center crop parameters
   - Check RGB conversion settings
   - Verify resolution configuration

## Future Improvements
1. Add support for additional camera modules
2. Implement more image processing features
3. Optimize memory usage
4. Add error recovery mechanisms
5. Enhance debugging capabilities

## Contributing
Please submit bug reports, feature requests, and pull requests through the project repository.

## License
This project includes components with various licenses. Please refer to individual source files for specific license information.
