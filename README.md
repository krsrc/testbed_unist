# KRSRC Testbed2 in UNIST

## Resources (SRCNet v0.1, following SRCNet format)
| Resource | Value | Expected Availability |
| --- | --- | --- |
| Storage | 279.5 TB (197TB for RSE) | 9/2024 |
|| 10*8 TB for user (HDD, CephFS) | H/W prepared |
|| 5*0.5 TB for OS (SSD) ||
| Compute | 11.26+alpha TFlops | 9/2024 |
|| 5*Gold 6338N ||
|| 1*Master ||
||| H/W prepared |
| Network | 10G, Internal ||
|| 1G, External -> 10G on discussion | 11/2024 |

## Resources (Lab)

1. ska00 (Desktop 1): for AAI
   - info: HDD 13TB, RAM 128GB, 16 cores
2. ska01 (Desktop 2): for master of Kubernetes cluster
   - info: HDD 33TB, RAM 256GB, 22 cores
3. ska02 (Desktop 3): for slave 1
   - info: HDD 25TB, RAM 256GB, 
4. ska03 (Desktop 4): for slave 2
   - info: HDD 17GB, RAM 128GB, 
5. ska04 (Desktop 5): for slave 3
   - info: HDD 17TB, RAM 128GB,
6. ska04 (Desktop 5): for slave 4
   - info: HDD, RAM, cores
 
## Milestones

- [ ] Install INDIGO IAM on ska00
- [ ] Connect INDIGO IAM and KAFE
- [ ] Install Kubernetes on ska01
- [ ] Install Rancher on ska01
- [ ] Install JupyterHub on ska01
- [ ] Connect INDIGO IAM and JupyterHub
- [ ] Install CANFAR on ska01

## Contributor

- Hyeseung Lee
- Hyunwoo Kang
