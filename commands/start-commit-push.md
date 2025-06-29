Prepare comprehensive commit and push for TESAIoT Platform release by:

1. Parse version from $ARGUMENTS
   - Expected format: vYYYY.MM-[beta|stable].XX
   - Extract version type (beta/stable) for branch selection

2. Display release preparation checklist:
```
🚀 TESAIOT PLATFORM RELEASE PREPARATION
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📦 Version: $ARGUMENTS
🌿 Target: [develop for beta | main for stable]
🔗 Repository: https://github.com/tesaiot/tesa-iot-platform

⚡ RELEASE CHECKLIST (DO NOT SKIP ANY ITEM):
```

3. Execute comprehensive release tasks:
```
☐ Update src/admin-ui-react/VERSION.txt
  - Set version to $ARGUMENTS
  - Run: make rebuild-ui
  - Restart services if needed

☐ Architecture & Documentation Updates
  - Summary latest architecture → CHANGELOG.md
  - Update TESAIoT_PLATFORM_KNOWLEDGE.md
  - Update ./TESA_Rules/NEXT_PLAN/ROADMAP_TO_PUBLIC_RELEASE.md

☐ Knowledge Documentation
  - Analyze successful implementations
  - Document in ./TESA_Rules/NEXT_PLAN/
  - Include Flowise, AI Assistant integrations
  - Define next version plan

☐ Version Files
  - Update VERSION.txt to $ARGUMENTS

☐ File Mapping Updates (if new files)
  - Update TESA_Rules/TESAIoT-FILE-MAPPING.md
  - Update tesaiot-file-mapping.txt

☐ Component Documentation
  - ACTIVE_COMPONENTS.md - current status
  - DEVELOPER_ONBOARDING_GUIDE.md
  - KNOWN_ISSUES.md
  - CHANGELOG.md - with version entry
  - FEATURES.md - new features
  - TODO.md - remaining tasks

☐ Security Documentation
  - DEVELOPER_ONBOARDING_GUIDE.md
  - CYBERSECURITY_FRAMEWORK_v2025.06.md
  - SECURITY_COMPLIANCE_REPORT.md
  - SECURITY_100_ROADMAP.md
  - Comprehensive cybersecurity updates

☐ Platform Documentation
  - README.md - latest version & capabilities
  - Both file mapping documents

☐ Git Operations
  - Stage ONLY necessary files (no temp/test)
  - Update .github/CI_CD_AND_DEPLOYMENT.md
  - Commit with message: "Release $ARGUMENTS"

☐ Push Strategy
  Beta: git push origin develop
       git tag -a $ARGUMENTS -m "Beta release $ARGUMENTS"
       git push origin $ARGUMENTS
  
  Stable: Create PR develop → main
          Tag after merge

☐ CI/CD Verification
  - Confirm workflows trigger correctly
  - Beta → develop branch workflows
  - Stable → main branch workflows

☐ Final Verification
  - Check README.md on GitHub
  - Verify version displayed correctly
  - Confirm all files updated
```

4. Get GitHub token and prepare push:
```bash
# Read GH_TOKEN from .env
source .env
echo "GitHub token loaded: ${GH_TOKEN:0:8}..."

# Configure git with token
git remote set-url origin https://${GH_TOKEN}@github.com/tesaiot/tesa-iot-platform.git
```

5. Execute git commands based on version type:
```bash
# For beta versions
if [[ $ARGUMENTS == *"beta"* ]]; then
  git checkout develop
  git pull origin develop
  # ... make all updates ...
  git add [necessary files only]
  git commit -m "Release $ARGUMENTS - Beta version with comprehensive updates"
  git push origin develop
  git tag -a $ARGUMENTS -m "Beta release $ARGUMENTS"
  git push origin $ARGUMENTS
fi

# For stable versions
if [[ $ARGUMENTS == *"stable"* ]]; then
  git checkout develop
  git pull origin develop
  # ... make all updates ...
  git add [necessary files only]
  git commit -m "Release $ARGUMENTS - Stable version ready for production"
  git push origin develop
  # Create PR from develop to main
  echo "Create PR from develop → main for stable release"
fi
```

6. Post-release verification:
```
✅ RELEASE CHECKLIST COMPLETED

📋 Verify:
- [ ] All documentation updated
- [ ] Version files correct
- [ ] GitHub shows latest changes
- [ ] CI/CD pipelines running
- [ ] Tags created (beta only)
- [ ] PR created (stable only)

🎯 Next Steps:
- Monitor CI/CD pipelines
- Check deployment status
- Announce release to team
```

7. Generate release notes summary:
```
## Release Notes for $ARGUMENTS

### Version Info
- Version: $ARGUMENTS
- Type: [Beta/Stable]
- Branch: [develop/main]
- Date: [current date]

### Updates Completed
- ✅ Platform version updated
- ✅ Documentation synchronized
- ✅ Security compliance reviewed
- ✅ Architecture documented
- ✅ File mappings updated

### Repository
https://github.com/tesaiot/tesa-iot-platform/releases/tag/$ARGUMENTS
```