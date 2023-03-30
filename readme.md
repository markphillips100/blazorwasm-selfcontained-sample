Repro steps - assumes power shell on windows

Either git clone and begin from step 3, or just follow the readme from step 1 without cloning and create a new project from scratch.  Note, the repo's project was created using SDK 7.0.202.

1. Create new wasm hosted app:

   ```
   dotnet new blazorwasm --hosted --use-program-main --no-https --name Samples.Sample1
   ````

2. Add a global.json to fix to SDK 7.0.202.

   ```
   {
      "sdk": {
          "version": "7.0.202"
      }
   }
   ```

3. F5 the Http configuration to test works by browsing to http://localhost:5000

4. Create Publish folder in repo root folder.

5. Publish to local folder without any `PublishSelfContained` command line property specified:

   ```
   dotnet publish -c Release .\Server\Samples.Sample1.Server.csproj -o .\Publish
   ```

6. Test the published app.  From a terminal change directory to the Publish folder, and type the following:

   ```
   dotnet .\Samples.Sample1.Server.dll
   ```

7. Browse to http://localhost:5000 once again and app should work fine as before.

8. Stop the server app from running, change directory from publish folder and empty the publish folder.  Want to ensure a clean publish.

9. Publish to local folder WITH `/p:PublishSelfContained=false` specified this time:

   ```
   dotnet publish -c Release /p:PublishSelfContained=false .\Server\Samples.Sample1.Server.csproj -o .\Publish
   ```

10. Repeat steps 6 & 7 and the browser should show an exception on startup of the wasm app.

11. Repeat step 8 & 9 with `/p:PublishSelfContained=true`, then repeat step 6 & 7 to test.  This time the app should work okay.

12. To prove a `/p:PublishSelfContained=false` setting used to work fine, modify the global.json to use SDK 7.0.104, and then repeat steps 8 & 9 to publish, and steps 6 & 7 to test:

    ```
    {
       "sdk": {
          "version": "7.0.104"
       }
    }
    ```
