# Fort Reign — EdgeOS Firewall Configuration Export
**Device:** EdgeRouter-X-SFP-6-Port (ERX-GW)
**IP:** 192.168.10.1 | **EdgeOS:** v3.0.1
**Export Date:** 2026-03-06
**Exported By:** Chris Robinson (CRobin0780)
**Method:** `show configuration commands | tee /home/ubnt/fortreign-edgeos-config.txt`

---

## Firewall Policy Summary

| Policy | Interface | Default | Purpose |
|--------|-----------|---------|---------|
| FW_VLAN10_IN | switch0.10 IN | DROP ✅ | MGMT inbound |
| FW_VLAN20_IN | switch0.20 IN | DROP ✅ | LAB inbound |
| FW_VLAN30_IN | switch0.30 IN | DROP ✅ | ATTACK inbound |
| FW_VLAN40_IN | switch0.40 IN | DROP ✅ | IoT inbound |
| WAN_IN | eth0 IN | DROP ✅ | Internet inbound |
| WAN_LOCAL | eth0 LOCAL | DROP ✅ | Internet to router |

---

## FW_VLAN10_IN — MGMT Inbound
| Rule | Action | Condition | Purpose |
|------|--------|-----------|---------|
| 10 | accept | state RELATED,ESTABLISHED | Return traffic |
| 20 | accept | daddr 192.168.20.0/24 | MGMT → LAB |
| 30 | drop | daddr 192.168.40.0/24 LOG | Block MGMT → IoT |
| 40 | drop | daddr 192.168.30.0/24 LOG | Block MGMT → Attack |
| 10000 | drop | default LOG | Fail-closed |

## FW_VLAN20_IN — LAB Inbound
| Rule | Action | Condition | Purpose |
|------|--------|-----------|---------|
| 10 | accept | state RELATED,ESTABLISHED | Return traffic |
| 20 | drop | daddr 192.168.10.0/24 | Block LAB → MGMT |
| 30 | accept | all | Allow LAB → Internet |
| 10000 | drop | default | Fail-closed |

## FW_VLAN30_IN — ATTACK Inbound
| Rule | Action | Condition | Purpose |
|------|--------|-----------|---------|
| 10 | accept | state RELATED,ESTABLISHED | Return traffic |
| 20 | drop | daddr 192.168.10.0/24 | Block Attack → MGMT |
| 30 | accept | daddr 192.168.20.0/24 | Allow Attack → LAB only |
| 10000 | drop | default LOG | Fail-closed |

## FW_VLAN40_IN — IoT Inbound
| Rule | Action | Condition | Purpose |
|------|--------|-----------|---------|
| 10 | drop | daddr 192.168.10.0/24 LOG | Block IoT → MGMT |
| 20 | drop | daddr 192.168.20.0/24 LOG | Block IoT → LAB |
| 30 | drop | daddr 192.168.30.0/24 LOG | Block IoT → Attack |
| 100 | accept | all | Allow IoT → Internet |
| 10000 | drop | default | Fail-closed |

---

## Change Log
| Date | Change | Operator |
|------|--------|----------|
| 2026-03-01 | FW_VLAN40_IN: IoT isolation, rules 10/20/30 drop RFC1918 | C. Robinson |
| 2026-03-06 | FW_VLAN10_IN: default ACCEPT→DROP, explicit ruleset added | C. Robinson |
| 2026-03-06 | FW_VLAN10_IN: removed permit-any rule 20, corrected conditions | C. Robinson |
