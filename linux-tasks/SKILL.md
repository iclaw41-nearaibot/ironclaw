---
name: linux-tasks
version: 0.1.0
description: Linux/Ubuntu system administration for the Contabo VPS. Process management, file ops, networking, cron jobs, systemd services, tmux, Ollama management, and server maintenance.
activation:
  patterns:
    - "linux.*"
    - "ubuntu.*"
    - "vps.*"
    - "server.*"
    - "ssh.*"
    - "systemd.*"
    - "cron.*"
    - "tmux.*"
    - "bash.*script"
  keywords:
    - "linux"
    - "ubuntu"
    - "vps"
    - "server"
    - "ssh"
    - "bash"
    - "systemd"
    - "cron"
    - "tmux"
    - "process"
    - "service"
    - "disk"
    - "memory"
    - "cpu"
  max_context_tokens: 2000
---

# Linux Tasks Skill

You manage the Contabo VPS (Ubuntu 24.04, 37.60.228.233) and any Linux environment.

## VPS Quick Reference
- **IP:** 37.60.228.233
- **User:** root
- **Connect:** `ssh root@37.60.228.233`
- **IronClaw path:** `/root/ironclaw`
- **Ollama model:** qwen3:8b

## System Monitoring

```bash
# CPU, memory, processes
htop
top -bn1 | head -20
free -h
df -h

# Who's eating CPU?
ps aux --sort=-%cpu | head -10
ps aux --sort=-%mem | head -10

# Disk usage by directory
du -sh /* 2>/dev/null | sort -rh | head -10

# Network
ss -tlnp           # listening ports
netstat -tulpn
curl ifconfig.me   # public IP
```

## Process Management

```bash
# Find and kill a process
pgrep -a ironclaw
pkill ironclaw
kill -9 <pid>

# Background a process
nohup ./ironclaw &
disown %1

# Check if service is running
systemctl status ironclaw
```

## tmux (keep sessions alive)

```bash
# New session
tmux new -s ironclaw

# Detach (leave running)
Ctrl+B, D

# Reattach
tmux attach -t ironclaw

# List sessions
tmux ls

# Kill session
tmux kill-session -t ironclaw

# Split pane horizontally
Ctrl+B, "

# Split pane vertically
Ctrl+B, %

# Switch pane
Ctrl+B, arrow key
```

## Systemd Services (run IronClaw on boot)

```bash
# Create service file
cat > /etc/systemd/system/ironclaw.service << 'EOF'
[Unit]
Description=IronClaw AI Agent
After=network.target ollama.service

[Service]
Type=simple
WorkingDirectory=/root/ironclaw
ExecStart=/root/ironclaw/target/release/ironclaw
Restart=always
RestartSec=10
EnvironmentFile=/root/.ironclaw/.env
StandardOutput=append:/var/log/ironclaw.log
StandardError=append:/var/log/ironclaw.log

[Install]
WantedBy=multi-user.target
EOF

# Enable and start
systemctl daemon-reload
systemctl enable ironclaw
systemctl start ironclaw
systemctl status ironclaw

# View logs
journalctl -u ironclaw -f
tail -f /var/log/ironclaw.log
```

## Cron Jobs

```bash
# Edit crontab
crontab -e

# Examples
# Every 3 hours — IronClaw heartbeat
0 */3 * * * /root/ironclaw/target/release/ironclaw heartbeat >> /var/log/ironclaw-heartbeat.log 2>&1

# Daily at 6am — backup config
0 6 * * * cp -r /root/.ironclaw /root/backups/ironclaw-$(date +\%Y\%m\%d)

# List cron jobs
crontab -l
```

## Ollama Management

```bash
# Check Ollama running
systemctl status ollama
curl http://localhost:11434/api/tags

# List models
ollama list

# Pull a model
ollama pull qwen3:8b
ollama pull llama3.2:3b

# Run model interactively
ollama run qwen3:8b

# Delete a model (free disk space)
ollama rm llama3

# Check context length
curl http://localhost:11434/api/show -d '{"name":"qwen3:8b"}' | python3 -m json.tool

# Ollama API test
curl http://localhost:11434/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"qwen3:8b","messages":[{"role":"user","content":"Hello"}]}'
```

## File Operations

```bash
# Copy files to VPS
scp file.txt root@37.60.228.233:/root/

# Copy from VPS
scp root@37.60.228.233:/root/file.txt .

# Sync directory
rsync -avz --progress ./ironclaw/ root@37.60.228.233:/root/ironclaw/

# Find files
find /root -name "*.log" -mtime +7  # logs older than 7 days
find /root -size +100M               # files over 100MB

# Archive
tar -czf backup.tar.gz /root/.ironclaw
tar -xzf backup.tar.gz
```

## Firewall (UFW)

```bash
ufw status
ufw allow 22    # SSH
ufw allow 80    # HTTP
ufw allow 443   # HTTPS
ufw enable
```

## Package Management

```bash
apt update && apt upgrade -y
apt install -y curl wget git tmux htop jq python3-pip
apt autoremove -y   # clean up unused packages
```

## Logs

```bash
# System logs
journalctl -f                    # follow all logs
journalctl -u ollama -f          # Ollama logs
journalctl --since "1 hour ago"

# App logs
tail -f /var/log/ironclaw.log
tail -100 /var/log/syslog
```

## Disk Cleanup

```bash
# Clear old logs
journalctl --vacuum-time=7d
apt autoremove -y && apt clean

# Docker cleanup (if installed)
docker system prune -af

# Find and delete large files
find /root -size +500M -type f
```
