## IBM Resilience (SOAR-APPHOST) Installation Guide

### Pre-Requisite:

| Requirements | Remarks |
|-------------|--------|
| APPHOST Version | 1.15.5.0.2 |
| File name | apphost-1.15.5.0.2.ova |
| Hardware Requirements | As specified in the shared design documents |
| SSL (Signed) | RootCA.pem, cert.pem, key.pem, and Intermediate.pem (if applicable) |
| FQDN | soarapp.<yourdomain> |
| Access Ports | 443, 65000, 65001 |

**Important Note:**  
Any values enclosed within angle brackets (`<>`) must be replaced with environment-specific information before proceeding.

This guide applies **only to AppHost Virtual Appliance (OVA) installations** and assumes **active internet connectivity**.

---

### a. Login to the SOAR APPHOST via CLI from ESXi console
1. Access the AppHost VM console from the ESXi management interface.
2. Follow the guided initialization prompts to configure:
   - Root and appadmin passwords
   - Network configuration (static/DHCP)
   - DNS and gateway settings

**Screenshot – Initial Console Configuration**  
![ESXi AppHost Console Setup](screenshot_apphost_console.png)

---

### b. Change the hostname and timezone
Configure the system hostname and ensure the correct regional timezone is set.

```bash
sudo hostnamectl set-hostname soarapp.<yourdomain>
sudo timedatectl set-timezone Asia/Kathmandu
```

**Screenshot – Hostname and Timezone Configuration**  
![Hostname and Timezone](screenshot_hostname_timezone.png)

---

### c. Install dependency packages
Install required system packages to support containerized AppHost services.

```bash
sudo dnf install container-selinux selinux-policy-targeted createrepo wget -y
```

---

### b. Login to SOAR and create pairing credentials
1. Log in to the IBM SOAR web console.
2. Navigate to **Administrative Settings**.
3. Generate AppHost pairing credentials.

**Screenshot – SOAR Administrative Settings**  
![SOAR Admin Settings](screenshot_soar_admin_settings.png)

---

### c. Navigate to Apps > Add +
1. Go to **Administrator Settings → Apps**.
2. Click **Add (+)** to register a new AppHost.

**Screenshot – Apps Section**  
![Apps Add AppHost](screenshot_apps_add.png)

---

### d. Add the AppHost name and generate pairing token
1. Enter the AppHost name.
2. Generate the pairing token.
3. Copy the generated token details.

**Screenshot – Add AppHost & Pairing Token**  
![Add AppHost Token](screenshot_add_apphost.png)

---

### e. Save pairing token on AppHost
Save the copied pairing information as `pair.json` inside the `/opt/` directory on the AppHost.

```bash
cd /opt/
# create pair.json and paste the copied content
```

**Screenshot – pair.json File Location**  
![pair.json Location](screenshot_pair_json.png)

---

### f. Pair the AppHost with SOAR
Execute the following command to complete the AppHost pairing process.

```bash
sudo manageAppHost install -p pair.json
```

**Screenshot – AppHost Pairing Execution**  
![AppHost Pairing](screenshot_pairing_command.png)

---

### g. Verify pods are running and healthy
Ensure all Kubernetes pods are running and reporting a healthy status.

```bash
kubectl get pods -A -w
```

All pods should display:
- **STATUS:** Running  
- **READY:** 1/1

**Screenshot – Kubernetes Pod Status**  
![Pods Running](screenshot_pods_running.png)

---

### h. Verify AppHost status in SOAR console
1. Log in to the SOAR administrative console.
2. Navigate to **Apps**.
3. Confirm the AppHost is listed and shows **Running** status.

**Screenshot – AppHost Running in SOAR**  
![AppHost Running](screenshot_apphost_running.png)

---

**The End**

