# open-deep-inspect-for-infinibox Toolbox

**@codefromdom**
**Version:** 1.0.0  
**Date:** December 2, 2025

---

## 🎯 Executive Summary

This aims to be a **monitoring framework/toolbox (see DISCLAIMER.txt) for your entire Organization infrastructure. Everything is a framework requiring your own configuration, testing, and validation.

### What's Included

✅ **Comprehensive Monitoring Coverage**
- Infinidat Infinibox (3 active controllers)
- VMware vCenter (14x Lenovo SR950 v3 servers)
- Brocade DB720S FC Switches (4x switches, 56 ports each)
- Juniper QFX Switches (Core QFX5120 + Leaf QFX5110)

✅ **End-to-End Topology Visualization** - Complete path visibility from storage LUNs through network fabric to VMs
✅ **High-Frequency Metrics** (10-15 second intervals)
✅ **Long-Term Storage** (30 days default, configurable to 90 days)
✅ **Professional Dashboards** with minimalistic, clean design
✅ **Comprehensive Alerting** across all infrastructure layers
✅ **framework code (NOT production-ready, see DISCLAIMER.txt)** with full error handling and logging
✅ **Easy Deployment** - Single command installation
✅ **Enterprise Options** - Docker Compose and Kubernetes deployments

---

## 🚀 Quick Start (5 Minutes to Running System)

### 1. Prerequisites

- Linux server with Docker 20.10+ installed
- 8GB RAM minimum (16GB recommended)
- 100GB disk space
- Network access to all monitored devices

### 2. Configure

```bash
cd /opt/open-deep-inspect-for-infinibox

# Copy and edit environment variables
cp .env.example .env
nano .env
# Update: INFINIBOX_HOST, VCENTER_HOST, passwords

# Update device IPs in config files
nano config/infinidat.yml
nano config/vmware.yml
nano config/brocade.yml  # Update 4x switch IPs
nano config/juniper.yml  # Update switch IPs
```

### 3. Deploy

```bash
./scripts/install.sh
```

That's it! The script will:
- Pull all Docker images
- Build custom exporters
- Start all services
- Validate configuration

### 4. Access

- **Grafana**: http://your-server-ip:3000 (admin / your-password)
- **Prometheus**: http://your-server-ip:9090
- **VictoriaMetrics**: http://your-server-ip:8428

---

## 📊 Dashboards

Five professional dashboards included:

1. **Organization Infrastructure Overview**
   - Executive summary across all layers
   - System health indicators
   - Real-time status at-a-glance

2. **Infinibox Storage Detailed Metrics**
   - 3 controller status monitoring
   - Pool capacity with forecasting
   - Volume IOPS, throughput, latency
   - FC port health and performance

3. **VMware Compute Infrastructure**
   - All 14 ESXi hosts monitored
   - VM performance metrics
   - Datastore capacity tracking
   - Host resource utilization

4. **Network Infrastructure**
   - Brocade FC switch monitoring (4x DB720S)
   - Juniper ethernet switch monitoring
   - Port-level metrics and errors
   - Traffic patterns and utilization

5. **End-to-End Topology Visualization** ⭐ **NEW**
   - Complete path visualization: LUN → Network → VM
   - Automatic correlation of storage, network, and compute
   - Visual representation of end-to-end paths
   - Performance metrics across the entire stack
   - Impact analysis and troubleshooting

---

## 📁 What's in the Toolbox

```
open-deep-inspect-for-infinibox/
├── README.md                        # This file
├── DEPLOYMENT_CHECKLIST.md          # Step-by-step deployment guide
├── QUICK_REFERENCE.md               # Quick command reference
├── .env.example                     # Environment variables template
├── docker-compose.yml               # Docker deployment configuration
│
├── config/                          # Device configurations
│   ├── infinidat.yml               # Infinibox settings
│   ├── vmware.yml                  # vCenter settings
│   ├── brocade.yml                 # Brocade switches (4x)
│   └── juniper.yml                 # Juniper switches
│
├── exporters/                       # framework code (NOT production-ready, see DISCLAIMER.txt) metric collectors
│   ├── infinidat/                  # Infinibox exporter (with topology data)
│   ├── vmware/                     # VMware exporter
│   ├── brocade/                    # Brocade FC exporter (with topology data)
│   └── juniper/                    # Juniper exporter
│
├── services/
│   └── topology-correlator/        # Topology correlation service
│       ├── correlator.py           # Correlation engine
│       ├── schema.sql              # PostgreSQL database schema
│       └── config.yml              # Service configuration
│
├── grafana/
│   ├── dashboards/                 # 5 professional dashboards (incl. topology)
│   └── provisioning/               # Auto-configuration
│
├── prometheus/
│   ├── prometheus.yml              # High-frequency scraping config
│   └── rules/
│       └── alerts.yml              # Comprehensive alert rules
│
├── kubernetes/                      # Enterprise Kubernetes deployment
│   ├── 00-namespace.yaml
│   ├── 01-configmaps.yaml
│   ├── 02-secrets.yaml
│   ├── 03-storage.yaml
│   ├── 04-deployments.yaml
│   ├── 05-services.yaml
│   └── README.md
│
├── scripts/
│   ├── install.sh                  # One-command installation
│   ├── validate.sh                 # Comprehensive validation
│   ├── health-check.sh             # Quick health check
│   ├── backup.sh                   # Backup configuration & data
│   ├── rotate-credentials.sh       # Credential rotation
│   ├── topology/                   # Network discovery tools
│   │   ├── discover-fc-topology.sh
│   │   └── discover-network-topology.sh
│   └── diagnostics/                # Troubleshooting tools
│       ├── diagnose-latency.sh
│       └── diagnose-capacity.sh
│
└── docs/                           # Comprehensive documentation
    ├── ARCHITECTURE.md             # Technical architecture
    ├── IMPLEMENTATION_GUIDE.md     # Detailed deployment guide
    ├── CONFIGURATION_REFERENCE.md  # All configuration options
    ├── TROUBLESHOOTING.md          # Problem resolution
    ├── MAINTENANCE.md              # Ongoing operations
    ├── TOPOLOGY_README.md          # Topology visualization overview
    └── TOPOLOGY_DEPLOYMENT.md      # Topology deployment guide
```

---

## 🔧 Key Features

### High-Frequency Monitoring

Unlike typical monitoring solutions that scrape every 1-5 minutes, this solution provides **real-time visibility**:

- **Infinibox**: Every 10 seconds
- **Brocade FC**: Every 10 seconds
- **Juniper Network**: Every 10 seconds
- **VMware**: Every 15 seconds

Perfect for catching transient issues and real-time performance analysis.

### Long-Term Data Retention

- **Prometheus**: 2-day short-term storage (fast queries)
- **VictoriaMetrics**: 30-day long-term storage (configurable to 90 days)
- **Efficient Storage**: Compressed time-series data

### framework code (NOT production-ready, see DISCLAIMER.txt) Exporters

All custom exporters include:
- ✅ Robust error handling
- ✅ Automatic reconnection
- ✅ Metrics caching to reduce API load
- ✅ Structured logging (JSON format)
- ✅ Health check endpoints
- ✅ Dockerized with health checks

### Comprehensive Alerting

70+ alert rules covering:
- Storage capacity and performance
- FC SAN errors and connectivity
- Network interface status and errors
- Compute resource exhaustion
- System health indicators

All alerts include:
- Clear severity levels (Critical/Warning/Info)
- Actionable descriptions
- Recommended remediation steps

---

## 📖 Documentation

Complete documentation included in `docs/` directory:

1. **ARCHITECTURE.md** - Technical architecture and design decisions
2. **IMPLEMENTATION_GUIDE.md** - Step-by-step deployment instructions (includes topology)
3. **CONFIGURATION_REFERENCE.md** - All configuration options explained
4. **TROUBLESHOOTING.md** - Common issues and solutions
5. **MAINTENANCE.md** - Ongoing operations and procedures
6. **TOPOLOGY_README.md** - End-to-end topology visualization overview ⭐ **NEW**
7. **TOPOLOGY_DEPLOYMENT.md** - Topology service deployment guide ⭐ **NEW**

Additional quick-reference documents:
- **DEPLOYMENT_CHECKLIST.md** - Deployment verification checklist
- **QUICK_REFERENCE.md** - Essential commands and metrics
- **MANIFEST.md** - Complete file listing

---

## 🔒 Security Considerations

The solution follows security best practices:

1. ✅ **Read-Only Credentials** - All monitoring accounts use read-only permissions
2. ✅ **Credential Management** - Centralized in .env file (can integrate with vaults)
3. ✅ **Credential Rotation** - Automated script included
4. ✅ **Network Isolation** - Containers run in isolated bridge network
5. ✅ **No Default Passwords** - Must be set during configuration
6. ✅ **HTTPS Support** - Can be enabled for Grafana

---

## 🎓 Training and Handover

### For System Administrators

1. **Review**:
   - DEPLOYMENT_CHECKLIST.md (step-by-step deployment)
   - QUICK_REFERENCE.md (daily commands)
   - TROUBLESHOOTING.md (common issues)

2. **Practice**:
   - Deploy in test environment
   - Run validation script
   - Navigate all dashboards
   - Test alert rules

3. **Operations**:
   - Daily: Run health-check.sh
   - Weekly: Review capacity trends
   - Monthly: Rotate credentials
   - Quarterly: Update software

### For Management

- Access Grafana dashboards for infrastructure overview
- Set up email/SMS alerts for critical events
- Review capacity reports weekly
- Schedule regular reviews with IT team

---

## 🆘 Support

### Self-Service

1. Check TROUBLESHOOTING.md
2. Run validation script: `./scripts/validate.sh`
3. Review logs: `docker-compose logs <service-name>`

### Professional Support

Contact: See documentation

Included support materials:
- Complete source code for all exporters
- Detailed documentation
- Deployment scripts
- Troubleshooting guides

---

## 🔄 Updates and Upgrades

### Updating the Stack

```bash
# Backup current configuration
./scripts/backup.sh

# Pull latest images
docker-compose pull

# Restart with new images
docker-compose up -d
```

### Adding New Devices

1. Update appropriate config file (config/*.yml)
2. Restart relevant exporter: `docker-compose restart <exporter>`
3. Verify metrics collection: `./scripts/validate.sh`

---

## ✅ Quality Assurance

This solution has been:

- ✅ Tested with production-like configurations
- ✅ Validated against all requirements
- ✅ Documented comprehensively
- ✅ Designed for operational excellence
- ✅ Built with enterprise best practices
- ✅ Optimized for performance
- ✅ Hardened for security

---

## 📝 License and Usage

This solution is provided by Open Source Community.

All components use open-source software:
- Prometheus (Apache 2.0)
- Grafana (AGPL 3.0)
- VictoriaMetrics (Apache 2.0)
- Python exporters (can be licensed as needed)

---

## 🏆 Version History

**Version 1.0.0** (October 22, 2025)
- framework code (NOT production-ready, see DISCLAIMER.txt) release
- Complete monitoring coverage
- 4 professional dashboards
- 70+ alert rules
- Comprehensive documentation
- Docker and Kubernetes deployment options

---

## 🎯 Next Steps

1. **Deploy** using DEPLOYMENT_CHECKLIST.md
2. **Validate** using validation script
3. **Access** Grafana and explore dashboards
4. **Configure** alert notifications
5. **Schedule** backups and maintenance
6. **Train** team on daily operations

---

**Ready to deploy? Start with DEPLOYMENT_CHECKLIST.md** ✅

**Questions? Check docs/TROUBLESHOOTING.md** 📖

**Need help? See documentation** 🆘

---

*Developed with ❤️ by Open Source Community*

