# Look at the interface

File Explorer CTRL SHIFT E

Search CTRL SHIFT F
Replace CTRL SHIFT H

Source Control CTRL SHIFT G

Debug CTRL SHIFT D

Extensions CTRL SHIFT X

Full Screen F11

Zen mode CTRL K Z

Look at the Extensions

You can install with chocolatey

choco install visualstudiocode --yes
choco install vscode-powershell --yes
choco install vscode-mssql --yes
choco install vscode-gitlens --yes

You can install the extensions with 

    # Install vscodeextensions module and extensions

    if ([version](Get-PackageProvider -Name nuGet).Version -le [version]2.8.5.201) {
        Write-Verbose "Installing Nuget"
        Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force
    }

    if (-not(Get-Module vscodeextensions -ListAvailable)) {
        Write-Verbose "Installing VS Code Extension"
        Install-Module vscodeextensions -Scope CurrentUser -Force
    }

    $VSCodeExtensions = 'material-theme-pack', 'bracket-pair-colorizer', 'powershell', 'mssql', 'gitlens'
    $VSCodeExtensions.ForEach{
            Write-Verbose "Installing VS Code Extension $psitem "
            Install-VSCodeExtension -ExtensionName $PSitem
        }


F1 to launch command pallete

Themes - make it look like ISE - Then change it back as ISE is horrible :-)

Look how easy it is to clone a repository

Clone this repo

https://github.com/SQLDBAWithABeard/JustARepo

Open the files look at the languages and the icons

Open the powershell file

We will come back to Problems

Output - look at the different types

Terminal

Integrated Console - Like ISE

Add a new terminal and another, split terminal and again

Show how to run powershell 6 in integrated and in normal

Delete - Move to the right and back down, split

Show insiders and F1 grid

Show the Settings - show how to set the default language

Show key bindings

Make a change showing intelliense, commit, push show logs

#region foreach database property
$a = Get-DbaDatabase -SqlInstance ROB-XPS
$TotalCmdlet = @()
$TotalStatement= @()
$TotalMethod = @()
0..10 | ForEach-Object {

$withcmdlet = Measure-Command {
$a | ForEach-Object {
 $psitem.AutoClose
}
}
    $TotalCmdlet += $withcmdlet 
    
$withstatement = Measure-Command {
foreach ($Beard in $a) {
        $Beard.AutoClose
}
}
    $TotalStatement += $withstatement

$WithMethod = Measure-Command {
    $A.ForEach{
            $psitem.AutoClose
    }
    }


$TotalMethod += $WithMethod
}

$MCCmdletAverage = ($TotalCmdlet | Measure-Object TotalMilliseconds -Average).Average
$MCStatementAverage = ($TotalStatement | Measure-Object TotalMilliseconds -Average).Average
$MCMethodAverage = ($TotalMethod | Measure-Object  TotalMilliseconds -Average).Average
cls
Write-Output "Average using ForEach Cmdlet = $MCCmdletAverage Milliseconds"
Write-Output "Average using ForEach Statement = $MCStatementAverage Milliseconds"
Write-Output "Average using With ForEach Method = $MCMethodAverage Milliseconds"

#endregion

Copy the code, show scriptanalyser rules green squiggles
Show Problems pane
Show auto formatting

Show code folding

then show splatting - how to install and how to use

Install-Module EditorServicesCommandSuite -Scope CurrentUser

# Place this in your VSCode profile
Import-Module EditorServicesCommandSuite
Import-EditorCommand -Module EditorServicesCommandSuite

Start-DbaMigration -Source $Source -Destination $Destination -BackupRestore -NetworkShare $Share -WithReplace -ReuseSourceFolderStructure -IncludeSupportDbs -NoAgentServer -NoAudits -NoResourceGovernor -NoSaRename -NoBackupDevices

then show mini map

Settings sync