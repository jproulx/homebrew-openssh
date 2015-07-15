openssh
=======
https://github.com/Homebrew/homebrew-dupes/pull/482#issuecomment-118994372

The dupes repo won't support keychain integration with openssh anymore, but I give no shits.

To use, simply do:

    brew tap jproulx/openssh
    brew install openssh-keychain 

once this completes, do:

    sudo nano /System/Library/LaunchAgents/org.openbsd.ssh-agent.plist    

locate the line (line 9 for me) that reads:

    <string>/usr/bin/ssh-agent</string>

and change it so it reads:

    <string>/usr/local/bin/ssh-agent</string>


Finally, add these lines to your .profile:

    eval $(ssh-agent)
    function cleanup {
        echo "Killing SSH-Agent"
        kill -9 $SSH_AGENT_PID
    }
    trap cleanup EXIT
