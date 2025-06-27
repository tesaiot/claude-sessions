# Claude Sessions - ระบบติดตามการพัฒนาโปรเจกต์แบบ Git Flow

## 📑 Table of Contents

- [ภาพรวม](#overview)
- [🌿 Git Flow Support](#git-flow-support)
- [คำสั่งที่ใช้ได้](#available-commands)
  - [🎯 คำสั่งหลัก (Basic Commands)](#basic-commands)
  - [🚀 คำสั่งเฉพาะ Branch (Branch-Specific Commands)](#branch-specific-commands)
  - [🔧 คำสั่ง Branch Management](#branch-management-commands)
- [โครงสร้างไฟล์](#file-structure)
- [การติดตั้ง](#installation)
- [📝 รายละเอียดคำสั่ง](#command-details)
  - [คำสั่งหลัก](#basic-command-details)
  - [คำสั่งเฉพาะ Branch](#branch-command-details)
  - [คำสั่ง Branch Management](#branch-management-details)
- [🔄 Session Recovery & Task Switching](#session-recovery)
  - [กรณี Claude หลุด/เครื่องดับ](#claude-disconnected)
  - [กรณีต้องการสลับไปทำงานอื่น](#task-switching)
  - [Session Lifecycle Management](#session-lifecycle)
- [🎯 Workflow Examples](#workflow-examples)
  - [Feature Development Flow](#feature-flow)
  - [Hotfix Flow](#hotfix-flow)
  - [Bug Fix Flow](#bugfix-flow)
  - [Improvement Flow](#improvement-flow)
- [💾 โครงสร้างไฟล์ Session แบบ Branch-Aware](#session-file-structure)
- [🛡️ Best Practices สำหรับ Session Management](#best-practices)
  - [การป้องกันการสูญเสีย Context](#prevent-context-loss)
  - [การจัดการหลาย Sessions](#manage-multiple-sessions)
  - [Session Naming Convention](#naming-convention)
  - [ควร Session-End เมื่อไหร่](#when-to-end-session)
- [💡 Tips & Tricks](#tips-and-tricks)
- [🚨 Troubleshooting](#troubleshooting)
- [📊 Session Metrics & Reports](#metrics-and-reports)
- [🔧 Advanced Configuration](#advanced-configuration)
- [🚀 ประโยชน์เพิ่มเติมจาก Git Flow Support](#git-flow-benefits)
- [🔧 การปรับแต่งเพิ่มเติม](#additional-customization)
- [📋 Quick Reference Card](#quick-reference)
- [🎓 Session Management Principles](#management-principles)
- [❓ FAQ - คำถามที่พบบ่อย](#faq)
- [📚 แหล่งข้อมูลเพิ่มเติม](#additional-resources)

---

<a name="overview"></a>
## ภาพรวม

คำสั่ง slash แบบกำหนดเองสำหรับ Claude Code ที่ช่วยติดตามและจัดทำเอกสารการพัฒนาอย่างครอบคลุม พร้อมรองรับ Git Flow workflow ระบบนี้ช่วยให้นักพัฒนาสามารถ:

- **บันทึกความคืบหน้า**: บันทึกสิ่งที่ทำ วิธีการทำ และเหตุผลในการตัดสินใจ
- **จัดการ Branch อัตโนมัติ**: สร้างและจัดการ feature, bugfix, improvement และ hotfix branches
- **ติดตามการเปลี่ยนแปลง**: ตรวจสอบการเปลี่ยนแปลงใน git, branch status, และ merge readiness
- **ถ่ายทอดความรู้**: ช่วยให้ session ในอนาคตเข้าใจงานที่ผ่านมาโดยไม่ต้องวิเคราะห์โค้ดทั้งหมดใหม่
- **เตรียมพร้อมสำหรับ PR**: สร้าง PR template และตรวจสอบความพร้อมก่อน merge

<a name="git-flow-support"></a>
## 🌿 Git Flow Support

ระบบรองรับ Git Flow workflow แบบเต็มรูปแบบ:

- **Default Branch**: `develop` - สำหรับการพัฒนาหลัก
- **Feature Branches**: `feature/*` - พัฒนา features ใหม่
- **Bugfix Branches**: `bugfix/*` - แก้ไข bugs ทั่วไป
- **Improvement Branches**: `improvement/*` - ปรับปรุงประสิทธิภาพและ refactoring
- **Hotfix Branches**: `hotfix/*` - แก้ไขด่วนสำหรับ production

<a name="available-commands"></a>
## คำสั่งที่ใช้ได้

<a name="basic-commands"></a>
### 🎯 คำสั่งหลัก (Basic Commands)

#### เริ่ม Session ใหม่
```bash
# เริ่ม session ทั่วไป (ถาม branch type)
/project:session-start authentication-refactor

# หรือไม่ใส่ชื่อ
/project:session-start
```

#### อัปเดตความคืบหน้า
```bash
# พร้อมหมายเหตุ
/project:session-update Implemented OAuth with Google

# หรือไม่ใส่หมายเหตุ (ระบบจะสรุปให้อัตโนมัติ)
/project:session-update
```

#### จบ Session
```bash
# สร้างสรุปที่ครอบคลุมพร้อม PR readiness check
/project:session-end
```

#### ดูสถานะ Session ปัจจุบัน
```bash
/project:session-current
```

#### แสดงรายการ Session ทั้งหมด
```bash
# แสดงแบบจัดกลุ่มตาม branch type
/project:session-list
```

#### แสดงคำแนะนำการใช้งาน
```bash
/project:session-help
```

<a name="branch-specific-commands"></a>
### 🚀 คำสั่งเฉพาะ Branch (Branch-Specific Commands)

#### Feature Development
```bash
# สร้าง feature branch จาก develop
/project:session-start-feature user-authentication
# → สร้าง branch: feature/user-authentication
```

#### Bug Fix
```bash
# สร้าง bugfix branch พร้อม issue number
/project:session-start-bugfix 123 fix-login-timeout
# → สร้าง branch: bugfix/123-fix-login-timeout
```

#### Improvement/Refactoring
```bash
# สร้าง improvement branch
/project:session-start-improvement optimize-database-queries
# → สร้าง branch: improvement/optimize-database-queries
```

#### Hotfix (Production)
```bash
# สร้าง hotfix branch จาก main
/project:session-start-hotfix 1.2.1 critical-security-patch
# → สร้าง branch: hotfix/1.2.1-critical-security-patch
```

<a name="branch-management-commands"></a>
### 🔧 คำสั่ง Branch Management

#### ตรวจสอบสถานะ Branch
```bash
# แสดงข้อมูล branch แบบละเอียด
/project:session-branch-status
```

#### Sync กับ Base Branch
```bash
# sync branch ปัจจุบันกับ base branch
/project:session-sync-branch
```

#### เตรียมพร้อมสำหรับ Review
```bash
# ตรวจสอบและสร้าง PR template
/project:session-ready-for-review
```

<a name="file-structure"></a>
## โครงสร้างไฟล์

```
.claude/
├── commands/                    # โฟลเดอร์คำสั่ง
│   ├── session-start.md        # คำสั่งเริ่ม session
│   ├── session-update.md       # คำสั่งอัปเดต session
│   ├── session-end.md          # คำสั่งจบ session
│   ├── session-current.md      # คำสั่งดูสถานะปัจจุบัน
│   ├── session-list.md         # คำสั่งแสดงรายการ sessions
│   ├── session-help.md         # คำสั่งแสดงความช่วยเหลือ
│   │
│   ├── session-start-feature.md     # สร้าง feature branch
│   ├── session-start-bugfix.md      # สร้าง bugfix branch
│   ├── session-start-improvement.md # สร้าง improvement branch
│   ├── session-start-hotfix.md      # สร้าง hotfix branch
│   │
│   ├── session-branch-status.md     # ดู branch status
│   ├── session-sync-branch.md       # sync กับ base branch
│   └── session-ready-for-review.md  # เตรียม PR

└── sessions/                    # โฟลเดอร์เก็บ session
    ├── .current-session        # ไฟล์ติดตาม session ที่ใช้งานอยู่
    ├── .config.json           # configuration file (optional)
    ├── 2025-01-16-1347-feature-auth.md
    └── [YYYY-MM-DD-HHMM-type-name].md
```

<a name="installation"></a>
## การติดตั้ง

### 1. Clone repository หรือคัดลอกโฟลเดอร์
```bash
git clone git@github.com:tesaiot/claude-sessions.git

# หรือคัดลอกโฟลเดอร์ .claude ไปยังโปรเจกต์
```

### 2. สร้างไฟล์ติดตาม sessions
```bash
mkdir -p .claude/sessions
touch .claude/sessions/.current-session
```

### 3. (Optional) สร้างไฟล์ configuration
```bash
cat > .claude/sessions/.config.json << EOF
{
  "defaultBranch": "develop",
  "branchTypes": {
    "feature": {
      "prefix": "feature/",
      "base": "develop",
      "target": "develop"
    },
    "bugfix": {
      "prefix": "bugfix/",
      "base": "develop",
      "target": "develop",
      "requireIssueNumber": true
    },
    "improvement": {
      "prefix": "improvement/",
      "base": "develop",
      "target": "develop"
    },
    "hotfix": {
      "prefix": "hotfix/",
      "base": "main",
      "target": ["main", "develop"],
      "requireVersion": true
    }
  }
}
EOF
```

### 4. เพิ่มใน .gitignore (ถ้าไม่ต้องการติดตาม)
```
.claude/sessions/
# หรือเก็บเฉพาะ config
.claude/sessions/*
!.claude/sessions/.config.json
```

<a name="command-details"></a>
## 📝 รายละเอียดคำสั่ง

<a name="basic-command-details"></a>
### คำสั่งหลัก

#### /project:session-start

**พารามิเตอร์:**
- `[name]` (ไม่บังคับ) - ชื่อบรรยาย session

**การทำงาน:**

- ตรวจสอบ branch ปัจจุบัน
- ถ้าอยู่บน main/master จะเตือน
- ถ้าอยู่บน develop จะถามประเภทงาน
- สร้างไฟล์ session พร้อม branch information
- อัปเดต `.current-session`

#### /project:session-update

**พารามิเตอร์:**

- `[notes]` (ไม่บังคับ) - หมายเหตุเกี่ยวกับการอัปเดต

**การทำงาน:**

- เพิ่มบันทึกความคืบหน้าพร้อม timestamp
- แสดง branch status (commits ahead/behind)
- เตือนถ้า branch ตกหลัง base branch
- บันทึก git changes และ todo progress
- สร้างสรุปอัตโนมัติถ้าไม่มีหมายเหตุ

#### /project:session-end

**การทำงาน:**

- สร้างสรุป session ที่ครอบคลุม
- เพิ่ม Branch & Merge Readiness section
- สร้าง PR template อัตโนมัติ
- แนะนำ next steps ตาม branch type
- ล้างไฟล์ `.current-session`

<a name="branch-command-details"></a>
### คำสั่งเฉพาะ Branch

#### /project:session-start-feature [name]

**การทำงาน:**

1. Checkout develop และ pull latest
2. สร้าง branch `feature/[name]`
3. สร้าง session พร้อม feature template
4. ถาม requirements และ acceptance criteria

#### /project:session-start-bugfix [issue] [name]

**การทำงาน:**

1. Checkout develop และ pull latest
2. สร้าง branch `bugfix/[issue]-[name]`
3. สร้าง session พร้อม bug details template
4. ถาม steps to reproduce

#### /project:session-start-improvement [name]

**การทำงาน:**

1. Checkout develop และ pull latest
2. สร้าง branch `improvement/[name]`
3. สร้าง session พร้อม improvement objectives
4. ถาม performance metrics (ถ้ามี)

#### /project:session-start-hotfix [version] [name]

**การทำงาน:**

1. ⚠️ Checkout main/master และ pull latest
2. สร้าง branch `hotfix/[version]-[name]`
3. สร้าง session พร้อม critical issue template
4. เตือนว่าจะ deploy ไป production

<a name="branch-management-details"></a>
### คำสั่ง Branch Management

#### /project:session-branch-status

แสดงข้อมูล:

- Branch type และ base branch
- Commits ahead/behind
- Local changes status
- Conflict detection
- Suggested actions

#### /project:session-sync-branch

ทำการ:

- Stash uncommitted changes
- Fetch และ merge base branch
- Handle conflicts (ถ้ามี)
- Apply stash back
- Update session log

#### /project:session-ready-for-review

ตรวจสอบ:

- All changes committed
- Branch up to date
- No conflicts
- Generate PR template
- Suggest reviewers

<a name="session-recovery"></a>
## 🔄 Session Recovery & Task Switching

<a name="claude-disconnected"></a>
### กรณี Claude หลุด/เครื่องดับ

#### วิธีกลับมาทำงานต่อ:
```bash
# 1. ตรวจสอบ session ที่ค้างอยู่
/project:session-current

# ถ้าไม่มี session (Claude ลืม context)
# 2. ดูรายการ sessions ล่าสุด
/project:session-list

# 3. Checkout กลับไปที่ branch
git checkout improvement/db-optimization

# 4. เริ่ม session ต่อ
/project:session-start db-optimization-continue

# 5. อ้างอิง session เก่า
/project:session-update Continuing from previous session [filename]
```

<a name="task-switching"></a>
### กรณีต้องการสลับไปทำงานอื่น

#### วิธีพัก Session ชั่วคราว:
```bash
# === พัก Improvement Work ===
# 1. Commit หรือ stash งานปัจจุบัน
git add .
git commit -m "WIP: Database optimization 60% complete"
# หรือ
git stash save "WIP: improvement work"

# 2. อัปเดตสถานะ
/project:session-update PAUSED - Switching to urgent feature. Progress: 60%

# 3. จบ session (mark as paused)
/project:session-end

# === เริ่มงานใหม่ ===
# 4. กลับไป develop
git checkout develop

# 5. เริ่ม feature ใหม่
/project:session-start-feature urgent-payment-fix

# === กลับมาทำต่อ ===
# 6. หลังเสร็จ feature
git checkout improvement/db-optimization

# 7. เริ่ม session ต่อ
/project:session-start db-optimization-resume

# 8. ดึงงานกลับ (ถ้า stash)
git stash pop
```

<a name="session-lifecycle"></a>

### Session Lifecycle Management

#### Session States
```
NEW → ACTIVE → PAUSED → RESUMED → COMPLETED
         ↓
      INTERRUPTED → RECOVERED
```

#### Session Lifecycle ที่แนะนำ:
```
Day 1: /project:session-start-feature user-auth
       /project:session-update [work]
       [ปิดเครื่อง - ไม่ต้อง end]

Day 2: /project:session-current (ยังเป็น ACTIVE)
       /project:session-update [continue work]
       [ปิดเครื่อง - ไม่ต้อง end]

Day 3: /project:session-update [finish work]
       /project:session-ready-for-review
       /project:session-end ← end ตอนพร้อม PR
```

<a name="workflow-examples"></a>

## 🎯 Workflow Examples

<a name="feature-flow"></a>

### Feature Development Flow
```bash
# 1. เริ่มพัฒนา feature
/project:session-start-feature payment-integration

# 2. พัฒนาและอัปเดต progress
/project:session-update Integrated Stripe API
/project:session-update Added webhook handlers

# 3. ตรวจสอบ branch status
/project:session-branch-status

# 4. Sync กับ develop ถ้าจำเป็น
/project:session-sync-branch

# 5. เตรียม PR
/project:session-ready-for-review

# 6. จบ session
/project:session-end
```

<a name="hotfix-flow"></a>

### Hotfix Flow
```bash
# 1. เริ่ม hotfix (จาก main)
/project:session-start-hotfix 1.2.1 fix-payment-bug

# 2. แก้ไขและทดสอบ
/project:session-update Fixed payment validation
/project:session-update Added regression tests

# 3. จบ session
/project:session-end
# → เตือน: merge ทั้ง main และ develop!
```

<a name="bugfix-flow"></a>

### Bug Fix Flow
```bash
# 1. เริ่ม bugfix พร้อม issue number
/project:session-start-bugfix 456 null-pointer-exception

# 2. วิเคราะห์และแก้ไข
/project:session-update Found root cause in UserService
/project:session-update Added null check and unit tests

# 3. ทดสอบ
/project:session-update All tests passing

# 4. จบ session
/project:session-end
```

<a name="improvement-flow"></a>

### Improvement Flow
```bash
# 1. เริ่ม improvement
/project:session-start-improvement api-response-optimization

# 2. Measure baseline
/project:session-update Baseline: 800ms average response time

# 3. ปรับปรุง
/project:session-update Implemented caching layer
/project:session-update Optimized database queries

# 4. Measure results
/project:session-update New: 200ms average (75% improvement)

# 5. จบ session
/project:session-end
```

<a name="session-file-structure"></a>

## 💾 โครงสร้างไฟล์ Session แบบ Branch-Aware

### ตัวอย่างไฟล์ Feature Session:
```markdown
# Feature Development Session - 2025-01-20 14:30 - user-authentication

## Branch Information
- Branch: feature/user-authentication
- Base Branch: develop
- Type: Feature Development
- Jira/Issue: AUTH-123

## Feature Requirements
- [x] User login with email/password
- [x] OAuth integration (Google)
- [ ] Two-factor authentication

## Acceptance Criteria
- [x] Users can register and login
- [x] Session management with JWT
- [ ] Remember me functionality

## Progress

### [14:30] Feature branch created
Created feature/user-authentication from develop (latest)

### [15:00] Implemented basic auth
**Branch Status**: 2 commits ahead, 0 behind develop
- Created auth middleware
- Added login/register endpoints
- Set up JWT tokens

### [16:30] Added Google OAuth
**Branch Status**: 5 commits ahead, 1 behind develop
⚠️ Need to sync with develop
- Integrated Google OAuth
- Updated user model
- Added OAuth callback handling

## Session Summary
[Generated by session-end]

### Branch & Merge Readiness
- Branch Type: Feature
- Current Branch: feature/user-authentication
- Merge Target: develop
- Branch Status: 8 commits ahead, 0 behind ✅
- Ready for PR: Yes

### Pre-Merge Checklist
- [x] All tests passing
- [x] No conflicts with base branch
- [x] Code reviewed locally
- [x] Documentation updated
```

<a name="best-practices"></a>
## 🛡️ Best Practices สำหรับ Session Management

<a name="prevent-context-loss"></a>
### การป้องกันการสูญเสีย Context
1. **Commit บ่อยๆ**: อย่างน้อยทุก 1-2 ชั่วโมง
2. **Update session สม่ำเสมอ**: บันทึกทุก milestone สำคัญ
3. **ใช้ descriptive messages**: อธิบายชัดเจนว่าทำอะไร
4. **Reference files**: ระบุไฟล์ที่แก้ไขใน updates

<a name="manage-multiple-sessions"></a>
### การจัดการหลาย Sessions
```bash
# ตรวจสอบ active sessions
/project:session-list

# ดู branch ทั้งหมดที่มี session
git branch | grep -E "(feature|bugfix|improvement|hotfix)"

# Clean up old branches
git branch -d feature/completed-feature
```

<a name="naming-convention"></a>
### Session Naming Convention
```
[TYPE]-[DESCRIPTION]-[STATUS]
- feature-auth-active
- bugfix-123-paused
- improvement-db-complete
- hotfix-1.2.1-merged
```

<a name="when-to-end-session"></a>
### ควร Session-End เมื่อไหร่

#### ✅ ควร end เมื่อ:
- งานเสร็จแล้ว 100%
- พร้อมจะ create PR
- ต้องการสลับไปทำงานอื่นนาน ๆ
- จบ milestone สำคัญ

#### ❌ ไม่ควร end เมื่อ:
- แค่พักเบรค/พักกลางวัน
- ปิดเครื่องตอนเย็น แต่พรุ่งนี้ทำต่อ
- งานยังไม่เสร็จ

<a name="tips-and-tricks"></a>
## 💡 Tips & Tricks

### 1. Quick Session Switch
```bash
# สร้าง alias สำหรับ switching
alias session-pause='git stash && /project:session-update "PAUSED for task switch"'
alias session-resume='git stash pop && /project:session-update "RESUMED work"'
```

### 2. Session Templates
สร้าง templates สำหรับ session types ที่ใช้บ่อย:

```bash
# .claude/templates/feature-template.md
# .claude/templates/bugfix-template.md
# .claude/templates/improvement-template.md
# .claude/templates/hotfix-template.md
```

### 3. Integration กับ Tools อื่นๆ
- Link กับ Jira/GitHub Issues
- Auto-update จาก CI/CD status
- Sync กับ project management tools

### 4. Automated Session Backup
```bash
# Backup sessions weekly
tar -czf sessions-backup-$(date +%Y%m%d).tar.gz .claude/sessions/

# หรือ sync ไป cloud
rsync -av .claude/sessions/ backup-server:/sessions/
```

<a name="troubleshooting"></a>
## 🚨 Troubleshooting

### Session ค้าง/หาย
```bash
# Reset session
rm .claude/sessions/.current-session
/project:session-start recovery

# Recover จาก git log
git log --oneline -20
# ดูว่าทำอะไรไปแล้ว
```

### Branch conflicts หลัง resume
```bash
# Update และ resolve
/project:session-sync-branch
# Follow prompts to resolve conflicts
```

### Multiple developers, same feature
```bash
# Use sub-branches
feature/auth-backend
feature/auth-frontend

# Or use initials
feature/auth-john
feature/auth-jane
```

### Session file corrupted
```bash
# Backup corrupted file
mv .claude/sessions/corrupted.md .claude/sessions/corrupted.md.bak

# Start fresh
/project:session-start recovery-from-corruption
```

<a name="metrics-and-reports"></a>

## 📊 Session Metrics & Reports

### Generate Session Report
```bash
# สร้างสรุปรายสัปดาห์
find .claude/sessions -name "*.md" -mtime -7 | xargs grep -h "Session Summary"

# นับ sessions ตาม type
ls .claude/sessions/*feature*.md | wc -l
ls .claude/sessions/*bugfix*.md | wc -l
ls .claude/sessions/*improvement*.md | wc -l
ls .claude/sessions/*hotfix*.md | wc -l
```

### Session Health Check
```bash
# ตรวจสอบ sessions ที่นานเกิน 7 วัน
find .claude/sessions -name "*.md" -mtime +7 -exec basename {} \;

# ตรวจสอบ branches ที่ไม่มี activity
git for-each-ref --format='%(refname:short) %(committerdate)' refs/heads/feature/
```

### Team Performance Metrics
```bash
# Average session duration
grep -h "Duration:" .claude/sessions/*.md | awk '{print $2}' | average

# Most productive day
grep -h "Session started" .claude/sessions/*.md | cut -d' ' -f1 | sort | uniq -c | sort -nr
```

<a name="advanced-configuration"></a>
## 🔧 Advanced Configuration

### .claude/sessions/.config.json (Full Example)
```json
{
  "defaultBranch": "develop",
  "sessionDefaults": {
    "autoCommitOnPause": true,
    "warnOnLongSessions": 7,
    "requireIssueLink": true,
    "autoBackup": true,
    "backupInterval": "daily"
  },
  "branchTypes": {
    "feature": {
      "prefix": "feature/",
      "base": "develop",
      "target": "develop",
      "template": "feature-template.md",
      "requireTests": true,
      "minCoverage": 80
    },
    "bugfix": {
      "prefix": "bugfix/",
      "base": "develop",
      "target": "develop",
      "requireIssueNumber": true,
      "template": "bugfix-template.md",
      "requireRegressionTest": true
    },
    "improvement": {
      "prefix": "improvement/",
      "base": "develop",
      "target": "develop",
      "template": "improvement-template.md",
      "requireBenchmark": true
    },
    "hotfix": {
      "prefix": "hotfix/",
      "base": "main",
      "target": ["main", "develop"],
      "requireVersion": true,
      "template": "hotfix-template.md",
      "urgentMode": true,
      "notifyTeam": true
    }
  },
  "integrations": {
    "jira": {
      "enabled": true,
      "projectKey": "PROJ",
      "autoLink": true
    },
    "slack": {
      "notifyOnSessionEnd": true,
      "channel": "#dev-updates",
      "mentionOn": ["hotfix", "critical"]
    },
    "github": {
      "autoCreatePR": false,
      "prTemplate": ".github/pull_request_template.md"
    }
  },
  "hooks": {
    "preSessionStart": "./scripts/pre-session.sh",
    "postSessionEnd": "./scripts/post-session.sh"
  }
}
```

<a name="git-flow-benefits"></a>
## 🚀 ประโยชน์เพิ่มเติมจาก Git Flow Support

1. **Branch Management อัตโนมัติ**: ไม่ต้องจำ naming convention
2. **ป้องกันข้อผิดพลาด**: เตือนเมื่อทำงานบน branch ที่ไม่เหมาะสม
3. **Merge Readiness**: ตรวจสอบความพร้อมก่อน create PR
4. **ติดตาม Branch Status**: รู้ตลอดว่า ahead/behind เท่าไหร่
5. **PR Template**: สร้าง description จาก session data
6. **Team Visibility**: ทุกคนเห็น progress ของทีม
7. **Knowledge Base**: สร้าง documentation อัตโนมัติ

<a name="additional-customization"></a>
## 🔧 การปรับแต่งเพิ่มเติม

### Custom Branch Types
สามารถเพิ่ม branch type ใหม่ใน `.config.json`:

```json
{
  "branchTypes": {
    "experiment": {
      "prefix": "exp/",
      "base": "develop",
      "target": "develop",
      "maxDuration": 14
    },
    "release": {
      "prefix": "release/",
      "base": "develop",
      "target": "main",
      "requireChangeLog": true
    }
  }
}
```

### Git Hooks Integration
สร้าง `.git/hooks/prepare-commit-msg`:

```bash
#!/bin/bash
# Auto-append session reference
SESSION=$(cat .claude/sessions/.current-session 2>/dev/null)
if [ ! -z "$SESSION" ]; then
  echo "" >> $1
  echo "Session: $SESSION" >> $1
fi
```

### Custom Commands
สร้างคำสั่งเพิ่มเติมใน `.claude/commands/`:

```markdown
# session-stats.md
Show statistics for current session including:
- Total commits
- Files changed
- Lines added/removed
- Time spent
- Productivity score
```

<a name="quick-reference"></a>
## 📋 Quick Reference Card

### Essential Commands
```bash
# Start work
/project:session-start-[type] [name]    # type: feature|bugfix|improvement|hotfix

# During work
/project:session-update [notes]          # Log progress
/project:session-branch-status          # Check branch health
/project:session-sync-branch            # Sync with base

# Switch tasks
git stash                               # Save work
/project:session-update PAUSED          # Mark pause
/project:session-end                    # End (keep branch)

# Resume work
git checkout [branch]                   # Return to branch
git stash pop                          # Restore work
/project:session-start [name]-continue  # Continue session

# Finish work
/project:session-ready-for-review       # Pre-PR check
/project:session-end                    # Final summary
```

### Branch Lifecycle
```
develop → feature/* → PR → develop
develop → bugfix/* → PR → develop  
develop → improvement/* → PR → develop
main → hotfix/* → PR → main + develop
```

### Quick Status Check
```bash
# Current status
/project:session-current

# Branch health
/project:session-branch-status

# All sessions
/project:session-list
```

<a name="management-principles"></a>
## 🎓 Session Management Principles

1. **One Session = One Purpose**: แต่ละ session ควรมีเป้าหมายชัดเจนเดียว
2. **Document Decisions**: บันทึกเหตุผลของการตัดสินใจสำคัญ
3. **Track Problems**: ปัญหาที่เจอวันนี้อาจช่วยคนอื่นพรุ่งนี้
4. **Complete Cycles**: ปิด session ทุกครั้งก่อนเริ่มใหม่
5. **Reference Previous Work**: อ้างอิง session เก่าเมื่อทำงานต่อ
6. **Keep It Simple**: ไม่ต้องบันทึกทุกรายละเอียด แต่บันทึกสิ่งสำคัญ
7. **Be Consistent**: ใช้รูปแบบเดียวกันทั้งทีม

<a name="faq"></a>
## ❓ FAQ - คำถามที่พบบ่อย

### Q: ต้อง session-end ทุกวันไหม?
**A**: ไม่จำเป็น! end เฉพาะเมื่องานเสร็จหรือต้องสลับไปทำอย่างอื่นนานๆ

### Q: Session หายหลัง Claude restart ทำไงดี?
**A**: ใช้ `/project:session-current` หรือ `/project:session-list` แล้วอ้างอิง session เก่า

### Q: ทำงานหลายคนบน feature เดียวกันได้ไหม?
**A**: ได้! ใช้ sub-branches เช่น feature/auth-backend, feature/auth-frontend

### Q: ลืม commit ก่อนสลับ branch ทำไงดี?
**A**: ใช้ `git stash` เก็บงานไว้ก่อน แล้ว `git stash pop` เมื่อกลับมา

### Q: Session file ใหญ่เกินไปทำไงดี?
**A**: พิจารณา end session แล้วเริ่มใหม่ หรือแยกเป็น sub-tasks

<a name="additional-resources"></a>
## 📚 แหล่งข้อมูลเพิ่มเติม

- **Repository**: https://github.com/tesaiot/claude-sessions
- **Git Flow Guide**: https://nvie.com/posts/a-successful-git-branching-model/
- **Claude Code Docs**: https://docs.anthropic.com/en/docs/claude-code/
- **Custom Commands**: https://docs.anthropic.com/en/docs/claude-code/slash-commands

---

*Claude Sessions - Making Development Tracking Effortless* 🚀