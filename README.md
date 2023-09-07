# SideCar_via_ssh
 A script wich starts Sidecar from an iPad

    After trying and failing a lot I finally found a solution to this problem! Version running on macOs Ventura 13.5

    I modified the script because it seems, that the Settings app is poorly supporting AppleScript, wich lead to a lot of issues. -> Script now not working with the settings app, but rather using the "Control Center" in the head bar of MacOs.

    tell application "System Events"
        
        tell its application process "ControlCenter"
            
            tell its menu bar 1
                -- click on and open Control Center drop down
                tell (UI elements whose description is "Kontrollzentrum")
                    click
                end tell
            end tell
            
            
            -- interact with Control Center window
            tell its window "Kontrollzentrum"
                delay 0.5
                -- click screen mirroring button
                set screenMirroringButton to button 2 of group 1
                -- click screenMirroringButton click doesn't work
                perform action 1 of screenMirroringButton
                delay 0.5
                set myScreen to checkbox 1 of its scroll area 1 of group 1
                perform action 1 of myScreen
            end tell
            
            
        end tell
    end tell

    Note that "Kontrollzentrum" is the german term for "Control Center", change it to term used by your system. In English it should be "Control Center".

    After I got this script to run in AppleScript I tried starting it from the iPad via a schortcut (run script via ssh). 
    The shortcut contains a single line of instruction:
    osascript ~Directory/scriptName.scpt

    After trying to start it I got an error on my iPad quoting:
    error: osaysscript ist not allowed assistive access (-1719) / osaysscript hat keine Berechtigungen für Hilfszugriff (-1719)

    You have to give BOTH Terminal as well as ssh-keygen-wrapper the rights to use assistive access:

    Open settings app -> go to Security Settings -> accessibility Settings -> give ssh-keygen-wrapper & terminal (maybe AppleScript as well, just to be sure) the rights!

    Einstellungen öffnen -> Datenschutz & Sicherheit -> Bedienungshilfen -> sshkeygen-wrapper & Terminal die Berechtigungen erteilen (zur Sicherheit auch AppleScript).

    Now it should work! Have fun!