# Display Utility

Linux utility to

1. Display information about the X11 desktop display like number of outputs, output names, current resolution and list of possible resolutions for all outputs using X11 and xrandr C libraries.
2. Capture screen as a RGB bitmap, encode using x264 and output continuous video frames.
3. Lock screen of any linux desktop using [lock-system](https://github.com/sindresorhus/lock-system) package.

## Usage

### Install from NPM to your dependencies

```console
npm install @idrive-remotepc/display-utility
```

### Import the various utilities as required from the package

#### Typescipt

```typescript
import { displayUtility, lockUtility, screenCaptureUtility } from '@idrive-remotepc/display-utility';
```

#### Javascript

```javascript
const { displayUtility, lockUtility, screenCaptureUtility } = require('@idrive-remotepc/display-utility');
```

## Functions exposed

### displayUtility.getConnectedOutputs(): number[] | undefined

Returns list of numbers which represents the RROutput corresponding to all the outputs.

### displayUtility.getOutputName(rROutput: number): string

Returns the name of the output (monitor) given the RROutput number for that output

### displayUtility.getCurrentResolution(rROutput: number): IResolution | undefined

Returns the current resolution of the output (monitor) given the RROutput number for that output

### displayUtility.getResolutions(rROutput: number): IResolution[] | undefined

Returns the list of possible resolutions for an output (montior) given the RROutput number for that output

### displayUtility.setResolution(rROutput: number, resolution: IResolution): void

Sets a particular resolution for an output (monitor) given the RROutput number for that output and the new resolution to be set.

### displayUtility.makeScreenBlank(): void

Reduces the brightness of all connected outputs to 0 and makes the screen blank.

### displayUtility.reverseBlankScreen(): void

Reverses the operation performed by makeScreenBlank()

### displayUtility.getPrimaryRROutput(): number

Get the RROutput number corresponding to the primary monitor

Note: When no monitor is marked as primary, one of the connected monitor's RROutput number is returned

### displayUtility.getExtendedMonitorResolution: IResolution | undefined

Get the complete resolution of the display when multiple monitors are connected.

Note: Returns same value as getCurrentResolution(), when single monitor is connected

### displayUtility.getAllCurrentResolutionsWithOffset(): IResolutionWithOffset[] | undefined

Get the position (x-offset and y-offset), height and width of connected monitors

### screenCaptureUtility.init(singleMonitorCapture: boolean, rROutput?: number): void

Initialises the screen capturer and x264 encoder for capturing screen.

To capture a single output (monitor) with RROutput number 65 (example):

```typescript
screenCaptureUtility.init(true, 65);
```

To capture the complete display including all connected outputs (monitors):

```typescript
screenCaptureUtility.init();
```

### screenCaptureUtility.getNextFrame(callback: (nextFrame: ArrayBuffer) => void): void

Returns the captured and encoded frame buffer as a callback.

```typescript
screenCaptureUtility.getNextFrame((frame: ArrayBuffer) => {
    // perform operation with frame
});
```

### lockUtility.lockScreen(): void

Locks the computer when executed

## Issues

Please feel free to raise issues on this repository, be it bugs or feature requests. We would be happy to address them.

## Debugging

Debugging the native node modules is possible using lldb extension in Visual Studio Code. Following are the steps:

1. Install recommended vscode extension vadimcn.vscode-lldb.
2. Install lldb in your system if it is not already installed.

    ```console
    # For debian
    apt install lldb

    # For RPM
    yum install lldb
    ```

3. Write required functions to debug in test.ts and start debugging using F5.
