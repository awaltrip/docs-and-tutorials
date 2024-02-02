# Debugging apps in VSCode or the browser

## Contents

1. Angular apps
    - [Debug in the browser](#Debug-Angular-in-the-browser)
    - [Debug in VSCode](#Debug-Angular-in-VSCode)
2. [Java Spring Boot apps](#java-spring-boot-apps)

## Angular apps

In order to debug an Angular app with breakpoints (whether you use the browser or VSCode), you must set an Angular build configuration with "sourceMap" set to true.

In `angular.json`:

```
"architect": {
  "build": {
    "configurations": {
      "local": {
        "sourceMap": true
      }
    }
  }
}

```
The configuration name can be "local", "dev" or whatever you'd like. It's common to see a "production" config in which case you want "sourceMap" to be false (source code should not be visible in production).

If you're working in an existing app, these configs are probably already set. Build the app with the correct config (e.g. `ng build --configuration=local`).

### Debug Angular in the browser

Debugging in the browser is not always the most effective, but it's simple.

1. Run your app and open `localhost:4200` (if an additional URL path is normally needed, include that).
2. Open the browser dev tools (CTRL+SHIFT+I).
3. Go to the Sources tab (Debugger tab in Firefox).
4. Press CTRL+P and begin typing the file name in which you'd like to place breakpoints.
5. Refresh the page to re-run the code if needed. When the code runs and hits your breakpoint, it should pause.
6. You can now view variable scope, call stack, and step over the function calls.

### Debug Angular in VSCode

It's sometimes preferable to debug directly in VSCode, as it's easier to read, easier to follow everything as you step through the code, and easy to make code changes immediately.

1. Many tutorials online suggest installing a browser extension for debugging. This is currently unnecessary / deprecated. VSCode now comes with a built in extension called **JavaScript Debugger** which works when running apps in Chrome or Edge.
    - For Firefox, install the VSCode extension **Debugger for Firefox**
2. In the Angular project, check the `.vscode` folder and see if there's a `launch.json` file. If not, create one.
3. Add the following code to the file (if there is not already a similar existing config).

    ```
    {
      "version": "0.2.0",
      "configurations": [
        {
          "name": "Launch Chrome",
          "type": "chrome",
          "request": "launch",
          "url": http://localhost:4200,
          "webRoot": "${workspaceFolder}"
        },
        {
          "name": "Attach Chrome",
          "type": "chrome",
          "request": "attach",
          "url": http://localhost:4200,
          "port": 9222,
          "webRoot": "${workspaceFolder}"
        }
      ]
    }
    ```
4. Some notes:
    - You can add additional objects for different browsers - use `"type": "edge"` or `"type": "firefox"`
    - In the "launch" object, if the app URL that you use to run the app includes a longer path (e.g. for ISP - `http://localhost:4200/#/personal/policy/policy-stub`), you can use that as the `"url"` value.
    - In the "attach" object, the "port" number is arbitrary - you can change it to something else if you want.
5. Run the app in a terminal as you normally would.
6. To launch the browser in debug mode, in VSCode press CTRL+SHIFT+D, choose your "launch" config in the dropdown on the top left, then click the green play button.
7. When your webpage loads, VSCode bottom toolbar should turn from blue to orange, and it should now include the debug toolbar towards the top. Refresh the page to re-run the code if needed. When the code runs and hits your breakpoint, it should pause.
8. You can now view variable scope, call stack, and step over the function calls.

#### You can also run your browser and _"attach"_ your debugger to it while it's running.

1. Run the app in a terminal as you normally would.
2. In Windows explorer or a new terminal, navigate to the folder containing the browser executable (e.g. Chrome executable is likely located in `C:\Program Files\Google\Chrome\Application`).
3. Open a new instance of your browser by running the command `chrome.exe --remote-debugging-port=9222` (replace the .exe with whatever browser .exe you need, and replace port # to match your `launch.json` if needed).
4. Navigate to your app at `localhost:4200/whatever-url-path-you-need`
5. In VSCode press CTRL+SHIFT+D, choose your "attach" config in the dropdown on the top left, then click the green play button.
6. VSCode bottom toolbar should turn from blue to orange, and it should now include the debug toolbar towards the top. Refresh the webpage to re-run the code if needed. When the code runs and hits your breakpoint, it should pause.
7. You can now view variable scope, call stack, and step over the function calls.

Issues with the debugger not responding can often be solved by refreshing the webpage, restarting the debugger, or restarting the browser.

## Java Spring Boot apps

For Spring Boot REST services, an effective way to debug is to "attach" a debugger from VSCode to an already running instance of the app.

1. Install the VSCode extension **Debugger for Java** if you don't already have it.
2. In the Spring Boot project, check the `.vscode` folder and see if there's a `launch.json` file. If not, create one.
3. Add the following code to the file (if there is not already a similar existing config).

    ```
    {
      "version": "0.2.0",
      "configurations": [
        {
          "name": "Attach Debugger",
          "type": "java",
          "request": "attach",
          "hostName": "localhost",
          "port": 9222
        }
      ]
    }
    ```
3. Note: the "port" number is arbitrary - you can change it to something else if you want.
4. Run the Spring Boot app with arguments - `mvn spring-boot:run -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=localhost:9222"`
    - make sure the `localhost:<port>` number in this command matches the one in `launch.json`.
    - if your app's run command already requires arguments, you'll have to combine them with this command.
    - terminal output when starting your app should now include `Listening for transport dt_socket at address: 9222`.
5. Once your app is running, in VSCode press CTRL+SHIFT+D, choose your "attach" config in the dropdown on the top left, then click the green play button.
6. VSCode bottom toolbar should turn from blue to orange, and it should now include the debug toolbar towards the top. When the code runs and hits your breakpoint, it should pause.
7. You can now view variable scope, call stack, and step over the function calls.
