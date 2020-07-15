# Flutter

## Summary

*Develop Flutter based applications. Includes the Flutter SDK, needed extensions, and dependencies.*

This definition is configured by default to work with Flutter Web development, but it includes all the tooling needed for android development, you only have to do some basic configuration at your host OS.

| Metadata | Value |  
|----------|-------|
| *Contributors* | Lucas |
| *Definition type* | Dockerfile |
| *Works in Codespaces* | Not tested |
| *Container host OS support* | Windows |
| *Languages, platforms* | Dart, Flutter |

### Topics
- [Using this definition with an existing folder](#Using-this-definition-with-an-existing-folder)
- [Testing the definition](#Testing-the-definition)
- [Container settings](#Container-settings)
- [Android development](#Android-development)


## Using this definition with an existing folder

This definition does not require any special steps to use. Just follow these steps:

1. If this is your first time using a development container, please follow the [getting started steps](https://aka.ms/vscode-remote/containers/getting-started) to set up your machine.

2. To use latest-and-greatest copy of this definition from the repository:
   1. Clone this repository.
   2. Copy the contents of `flutter-dev-container/.devcontainer` to the root of your project folder.
   3. Start VS Code and open your project folder.

4. After following last step, the contents of the `.devcontainer` folder in your project can be adapted to meet your needs.

5. Finally, press <kbd>F1</kbd> and run **Remote-Containers: Reopen Folder in Container** to start using the definition.

## Testing the definition

This definition includes some test code that will help you verify it is working as expected on your system. Follow these steps:

1. If this is your first time using a development container, please follow the [getting started steps](https://aka.ms/vscode-remote/containers/getting-started) to set up your machine.
2. Clone this repository.
3. Start VS Code, press <kbd>F1</kbd>, and select **Remote-Containers: Open Folder in Container...**
4. Select the `flutter-dev-container` folder.
5. After the folder has opened in the container, press <kbd>F5</kbd> to start the project and launch the browser.
6. You should see Counter App example after the page loads.
7. From here, you can edit the contents of the `test-project` folder to do further testing.
> If your're using Chrome as default browser, it will load a white page, to fix this you need to install the [Dart Debug Extension](https://chrome.google.com/webstore/detail/dart-debug-extension/eljbmlghnomdjgdjmbdekegdkbabckhm).

## Container settings

At the start of the Dockerfile you can setup things related to the SDKs used, for that change the value of the ENV variables.
```
#
# Android SDK
# https://developer.android.com/studio#downloads
ENV ANDROID_SDK_TOOLS_VERSION 6514223
ENV ANDROID_PLATFORM_VERSION 29
ENV ANDROID_BUILD_TOOLS_VERSION 29.0.3
ENV ANDROID_HOME=/opt/android-sdk-linux
ENV ANDROID_SDK_ROOT="$ANDROID_HOME"
ENV PATH=${PATH}:${ANDROID_HOME}/cmdline-tools/tools/bin:${ANDROID_HOME}/platform-tools:${ANDROID_HOME}/emulator

#
# Flutter SDK
# https://flutter.dev/docs/development/tools/sdk/releases?tab=linux
ENV FLUTTER_CHANNEL="beta"
ENV FLUTTER_VERSION="1.19.0-4.3.pre"
# Set this variable as "enable" to auto config flutter web-server.
# Make sure to use the needed channel and version for this.
ENV FLUTTER_WEB="enable"
ENV FLUTTER_HOME=/opt/flutter
ENV PATH=${PATH}:${FLUTTER_HOME}/bin
```
Remember that for work with flutter web you should use the Beta channel

## Android development

### Linux
Connect your physical Android device to your system via USB port.
Set the connection mode to PTP or File transfer inside the mobile device.
Run `flutter doctor` from the Docker container terminal.
> If you do not see the green check mark, then it might be that you have adb running on the host machine and it has connected to it. An ADB daemon running on the device cannot be connected to two ADB servers. So, on the host machine, run this command to disconnect from ADB:
`adb kill-server`

Now you should be able to connect to the device using the ADB on Docker.

### MacOS and Windows
You can't share your USB with dev container on macOS and Windows, but this link can be done using adb over TCP/IP, for that you should have `adb` installed on you host OS. The `adb` comes with the SDK Platform-Tools, which can be downloaded from [here](https://developer.android.com/studio/releases/platform-tools#downloads).

Connect your Android device to the system (make sure debug mode is turned on).

1. Run the following command to see the list of connected devices: ```adb devices```
2. Run the following commands to connect to the device wirelessly: 
    ```
    adb tcpip 5555
    adb connect 192.168.0.5:5555
    adb devices
    ```
    > Replace the IP address with that of the WiFi the mobile device is connected to. You can get it by going to WiFi Settings -> Advanced on your mobile device.
    
    > NOTE: Both the mobile device and the system should be connected to the same network.
    
    > You will see that both the usb connected device and the wirelessly connected device are displayed.
3. Disconnect the device connected via USB cable, and again run the command `adb devices` to verify whether the device is still connected wirelessly.
4. Now, run the Docker container inside VS Code.
5. From the container, run this command to check if any device is connected:
	`adb devices`
    > You will get an empty list.
6. Then run the following command:
	```
    adb connect 192.168.0.5:5555
	adb devices
    ```
    > Use the same IP address and port number you specified before while connecting to `adb` from your system.

    > Also, make sure that you allow USB debugging when the pop-up comes on the device.
7. In the previous step, you might get device unauthorized. To fix that, run:
	```
    adb kill-server
	adb connect 192.168.0.5:5555
	adb devices
    ```
    > Now you will see that the unauthorized error is gone.
8. Run `flutter doctor` once to verify that the device is recognized by Flutter.

## License

Licensed under the MIT License. See [LICENSE](https://github.com/lucashilles/flutter-dev-container/blob/master/LICENSE).
