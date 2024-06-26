Official Documentation

https://tljh.jupyter.org/en/latest/install/custom-server.html
https://jupyterlab-realtime-collaboration.readthedocs.io/en/latest/index.html
https://dashboard.ngrok.com/get-started/setup/linux

1. WSL

    Before we install jupyter lab or jupyter hub we need install or enable windows subsystem for linux
    on terminal windows:
    ```consloe
    dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
    ```
    and then we need enable Virutal Machine
    on terminal windows:
    ```consloe
    dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
    ```
    Install Ubuntu
    on terminal windows:
    ```consloe
    wsl --list --online
    wsl --install Ubuntu-20.04
    ```

2. Jupyter Hub

    Configure Network's

    on terminal windows:
    ```consloe
    netsh interface ip add address "vEthernet (WSL)" 192.168.10.1 255.255.255.0
    netsh interface portproxy add v4tov4 listenport=80 listenaddress=0.0.0.0 connectport=80 connectaddress=192.168.10.1
    ```
    on terminal wsl
    ```consloe
    sudo apt update
    sudo ip addr add 192.168.10.2/24 broadcast 192.168.10.255 dev eth0 label eth0:1;
    ```

    Install Python and Jupyter Hub
    on terminal wsl:
    ```consloe
    sudo apt install python3 python3-dev git curl -y
    curl -L https://tljh.jupyter.org/bootstrap.py | sudo -E python3 - --admin babat
    ```
    Check ipaddress in the WSL:
    ```console
    ifconfig
    ```
    Open browser on windows and then check the ipaddress if jupyter hub is serving...

3. Install Nvidia Driver to WSL

    Open Terminal in the Jupyter Notebook

    ```consloe
    !nvidia-smi
    ```
    check if nvidia driver installed on the WSL

    if not installed:
    ```consloe
    sudo apt install nvidia-utils-535 -y
    ```

4. Install Jupyter Collabroation
    Open Terminal in the Jupyter Notebook
    ```consloe
    sudo -E conda install -c conda-forge jupyter-collaboration
    ```

    after this installation you need to restart the WSL

    if successfuly installed you will see indicator 'RTC' in the notebook

5. Share Notebook Over Internet

    ```consloe
    curl -o ngrok.zip https://bin.equinox.io/c/bNyj1mQVY4c/ngrok-v3-stable-linux-amd64.tgz

    sudo tar -xvzf ngrok.zip -C /usr/local/bin

    ngrok config add-authtoken <your authtoken>

    ngrok http http://localhost:80
    ```
    Test the URL that ngrok serve