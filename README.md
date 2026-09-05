# 🚨 Caso de Estudio SOC: Análisis de Incidente por Phishing y C2 (Command & Control)

## 📌 Resumen del Incidente
Se detectó tráfico anómalo en el EDR/SIEM correspondiente al equipo del área de Finanzas (`192.168.1.45`), con conexiones salientes periódicas (beaconing cada 30s) hacia la IP externa `185.220.101.5` (`updates-check-sec.com`).

---

## 🔍 Vectores de Ataque e Indicadores de Compromiso (IoCs)

* **Vector de Entrada:** Phishing táctico mediante ingeniería social. Enmascaramiento de ejecutable con doble extensión (`Factura_Pendiente_Agosto.pdf.exe`).
* **Mecanismo de Persistencia:** Modificación de la clave de registro `HKCU\Software\Microsoft\Windows\CurrentVersion\Run` para asegurar ejecución automática tras cada reinicio del sistema (MITRE ATT&CK T1547.001).
* **User-Agent Sospechoso:** `Mozilla/5.0 (Windows NT 10.0; Win64; x64) PowerShell/7.1` (Invocación de scripts PowerShell desde el ejecutable).

---

## 🛡️ Playbook de Respuesta a Incidentes (Triaje en Terreno)

1. **Contención de Endpoint (Aislamiento):**
   * Desconexión física e islación lógica del host `192.168.1.45` de la red VLAN local para evitar movimiento lateral o exfiltración activa.

2. **Contención Perimetral:**
   * Bloqueo inmediato de la IP `185.220.101.5` y del dominio `updates-check-sec.com` en las reglas salientes del Firewall perimetral.

3. **Análisis y Threat Intelligence:**
   * Extracción de la muestra del ejecutable para obtención de HASH (SHA256) y consulta en VirusTotal.
   * Limpieza de la clave de Registro afectada y erradicación del artefacto.

---

## 👤 Analista SOC Nivel 1
* **Bastián Gallardo** - *Blue Team Analyst*
