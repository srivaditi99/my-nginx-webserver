# my-nginx-webserver
My local Nginx web server

## Install and run Nginx on Windows as a service

1. Download Nginx
   - Visit https://nginx.org/en/download.html
   - Download the latest Windows package (`nginx-<version>.zip`)
   - Extract to `C:\Program Files\Nginx\nginx-1.30.2\`

2. Configure Nginx for port 80
   - Open `C:\Program Files\Nginx\nginx-1.30.2\conf\nginx.conf`
   - In the `server` block, verify `listen 80;`

3. Test the configuration
   - Open PowerShell or Command Prompt as Administrator
   - Run:
     - `cd C:\Program Files\Nginx\nginx-1.30.2\`
     - `.\nginx.exe -t`
   - Confirm `syntax is ok` and `test is successful`

4. Install Nginx as a Windows service using NSSM
   - Download NSSM from https://nssm.cc/download
   - Extract and copy `nssm.exe` to `C:\nssm\nssm.exe`
   - Run as Administrator:
     - `C:\nssm\nssm.exe install nginx "C:\Program Files\Nginx\nginx-1.30.2\nginx.exe"`
   - Or run `C:\nssm\nssm.exe install nginx` and set:
     - Application path: `C:\Program Files\Nginx\nginx-1.30.2\nginx.exe`
     - Startup directory: `C:\Program Files\Nginx\nginx-1.30.2`

5. Start and manage the service
   - `C:\nssm\nssm.exe start nginx`
   - Or open `services.msc`, find `nginx`, and start it

6. Verify it is running
   - Open `http://localhost`
   - Or run `curl http://localhost`

## Run Nginx at login without a Windows service

If you want Nginx to start automatically when you log in without installing it as a Windows service, use one of these options.

### Option 1: From Command prompt

1. Run command prompt as administrator
2. Go to folder `C:\Program Files\Nginx\nginx-1.30.2`
3. Run the following at command prompt `.\nginx.exe`
4. Minimize the command prompt window


### Option 2: Startup folder

1. Open File Explorer and go to `C:\ProgramData\Microsoft\Windows\Start Menu\Programs\StartUp`
   - Or press `Win + R` and enter `shell:startup`
2. Create a new shortcut
   - Target: `C:\Program Files\Nginx\nginx-1.30.2\nginx.exe`
   - Start in: `C:\Program Files\Nginx\nginx-1.30.2`
3. Save the shortcut.

Nginx will launch automatically when you sign in.

### Option 3: Task Scheduler

1. Open `Task Scheduler`
2. Create a new task and name it `Start Nginx`
3. In the `General` tab:
   - Choose `Run only when user is logged on`
   - Optionally check `Run with highest privileges` if needed
4. In the `Triggers` tab:
   - Add a trigger for `At log on` for your user account
5. In the `Actions` tab:
   - Action: `Start a program`
   - Program/script: `C:\Program Files\Nginx\nginx-1.30.2\nginx.exe`
   - Start in: `C:\Program Files\Nginx\nginx-1.30.2`
6. Save the task.

This starts Nginx without registering it as a Windows service.

> Note: Running on port 80 requires Administrator privileges. If port 80 is already in use, stop any conflicting service (IIS, W3SVC, Skype, etc.).

