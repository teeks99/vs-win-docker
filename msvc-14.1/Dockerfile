#escape=`
FROM mcr.microsoft.com/dotnet/framework/sdk:4.8-windowsservercore-ltsc2019

# Restore the default Windows shell for correct batch processing.
SHELL ["cmd", "/S", "/C"]

ADD https://aka.ms/vs/15/release/vs_buildtools.exe C:\TEMP\vs_buildtools.exe

# These options require 30GB+ of space on the docker image, which is higher than the default of 20GB
# In the docker engine config, dockerd.json, add a json line `"storage-opts": ["size=40G"],`
# This command is only successful when run with `-m 4g` for 4GB of RAM
RUN powershell -Command Start-Process -PassThru -Wait -FilePath "C:\TEMP\vs_buildtools.exe" -ArgumentList `
    '--quiet','--wait','--norestart','--nocache','--includeRecommended',`
    '--add','Microsoft.VisualStudio.Workload.MSBuildTools',`
    '--add','Microsoft.VisualStudio.Workload.VCTools',`
    '--add','Microsoft.VisualStudio.Component.VC.ATL',`
    '--add','Microsoft.VisualStudio.Component.VC.ATLMFC',`
    '--add','Microsoft.VisualStudio.Component.VC.CLI.Support',`
    '--add','Microsoft.VisualStudio.Component.Windows10SDK.10586'

# Define the entry point for the docker container.
# This entry point adds the developer environemnt and starts the command shell
ENTRYPOINT ["C:\\Program Files (x86)\\Microsoft Visual Studio\\2017\\BuildTools\\Common7\\Tools\\VsDevCmd.bat", `
    "&&", "cmd.exe"]

