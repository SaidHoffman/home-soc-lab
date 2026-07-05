# Fase 0 — Cimientos del laboratorio

**Objetivo:** dejar operativo el SIEM y un primer endpoint enviando telemetría.
**Resultado:** ✅ Wazuh desplegado, endpoint Windows enrolado y **Active**, Sysmon alimentando el SIEM con las primeras detecciones visibles.

---

## 0.1 — Hipervisor

- **VMware Workstation Pro** (gratis para uso personal desde nov-2024, sin licencia).
- Requisito: virtualización (VT-x / AMD-V) habilitada en BIOS/UEFI.
- Nota: con Hyper-V / WSL2 / Docker Desktop activos, VMware corre sobre el hipervisor de Windows (algo más lento, pero funciona).

## 0.2 — SIEM (Wazuh OVA)

1. Descargar el OVA de Wazuh (v4.14.x) desde `wazuh.com/install` → *Virtual Machine (OVA)*.
2. En VMware: **File → Open** → importar el `.ova`.
3. Ajustes de la VM: **6 GB RAM**, **2 vCPU**, red **NAT**.
4. **Fix para CPU AMD** (el OVA se congela en el splash al arrancar en procesadores AMD): editar el archivo `.vmx` de la VM (con la VM apagada) y añadir al final el bloque de compatibilidad de CPUID + `featureCompat.enable = "FALSE"`. Ver [`../config/wazuh/vmware-amd-fix.vmx.txt`](../config/wazuh/vmware-amd-fix.vmx.txt).
5. Encender. Login de consola: usuario `wazuh-user` / contraseña `wazuh`.
6. Obtener la IP con `ip a` (interfaz `eth0`).
7. Acceder al dashboard desde el host: `https://<IP>` → usuario `admin` / contraseña `admin`.

> 🔐 **Cambiar de inmediato las contraseñas por defecto.** Nunca subir credenciales reales al repositorio.

## 0.3 — Endpoint Windows + agente + Sysmon

### 0.3a — Agente Wazuh
1. En el dashboard: **Deploy new agent**.
2. Paquete **Windows (MSI)**; *Server address* = IP del manager; nombre de agente = `win-host`.
3. Copiar el comando de PowerShell generado y ejecutarlo en **PowerShell como Administrador**.
4. Arrancar el servicio: `NET START WazuhSvc`.
5. Verificar en **Endpoints**: el agente aparece **Active**.

### 0.3b — Sysmon (telemetría enriquecida)
1. Descargar **Sysmon** (Sysinternals) y una config sólida (SwiftOnSecurity `sysmonconfig-export.xml`).
2. Instalar (PowerShell Admin):
   ```powershell
   .\Sysmon64.exe -accepteula -i sysmonconfig-export.xml
   ```
3. Indicar al agente que lea el canal de Sysmon: añadir a `C:\Program Files (x86)\ossec-agent\ossec.conf` (antes de `</ossec_config>`) el bloque de [`../config/wazuh/ossec-agent-sysmon.xml`](../config/wazuh/ossec-agent-sysmon.xml).
4. Reiniciar el agente: `Restart-Service WazuhSvc`.

## Verificación

Se generó actividad de prueba en el endpoint (comandos de PowerShell) y se confirmó en el dashboard (**Threat Hunting**, filtrando por `agent.name: "win-host"`) la llegada de eventos de Sysmon, incluyendo grupos de reglas `sysmon`, `sysmon_eid1_detections` (creación de proceso) y alertas de actividad de PowerShell y *discovery*.

## Estado final de la Fase 0

- ✅ SIEM Wazuh operativo y accesible.
- ✅ Endpoint Windows enrolado y **Active**.
- ✅ Sysmon enviando telemetría al SIEM.
- ✅ Primeras detecciones visibles y filtrables por endpoint.
