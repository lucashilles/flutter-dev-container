# Flutter

## Summary

*Develop Flutter based applications. Includes the Flutter SDK, needed extensions, and dependencies.*

| Metadata | Value |  
|----------|-------|
| *Contributors* | Lucas |
| *Definition type* | Dockerfile |
| *Works in Codespaces* | Not tested |
| *Container host OS support* | Windows |
| *Languages, platforms* | Dart, Flutter |

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
6. You should see "Hello remote world!" after the page loads.
7. From here, you can add breakpoints or edit the contents of the `test-project` folder to do further testing.

## License

Licensed under the MIT License. See [LICENSE](https://github.com/lucashilles/flutter-dev-container/blob/master/LICENSE).
