# 🧪 IntelSoft LMS Comprehensive Testing Guide

## Executive Summary

**Testing Objective:** Systematically identify and document all issues in the IntelSoft LMS platform to ensure production readiness.

**Test Environment:**

- URL: https://lms-demo.intelsoft.sg/
- Credentials: sandboxcm / Changeme!1
- Browser: Chrome (primary), Firefox/Safari (secondary)
- Duration: 45-60 minutes

**Critical Success Factors:**

- Identify all blocking issues before production deployment
- Document issues with screenshots and reproduction steps
- Prioritize fixes based on user impact and severity

---

## 📋 Pre-Test Checklist

### Environment Setup

- [ ] Chrome browser installed and updated
- [ ] Developer Tools enabled (F12)
- [ ] Screenshot tool ready (Win+Shift+S or browser tools)
- [ ] Clear browser cache (Ctrl+Shift+R)
- [ ] Test credentials verified

### Documentation Ready

- [ ] This testing guide printed/opened
- [ ] Issue tracking template ready
- [ ] Screenshot naming convention understood
- [ ] Timer/stopwatch for performance testing

---

## 🎯 Phase 1: Critical Path Testing (20 minutes)

### 1.1 Public Homepage Assessment (3 minutes)

**Objective:** Verify public-facing content quality

**Steps:**

1. Navigate to https://intelsoft.info (without /my/)
2. Observe homepage content for 30 seconds
3. Check slideshow banners for placeholder text
4. Note any unprofessional content

**Expected Results:**

- Professional, relevant content
- No Lorem ipsum placeholder text
- Clear value proposition

**Issue Indicators:**

- Lorem ipsum text in banners
- Generic or incomplete content
- Broken images or links

**Documentation:**

- Screenshot: `issue_public_homepage_placeholder_[timestamp].png`
- Severity: HIGH (visible to all visitors)

---

### 1.2 Authentication Testing (5 minutes)

**Objective:** Verify login functionality and session management

**Test Cases:**

#### TC-AUTH-001: Valid Login

**Steps:**

1. Navigate to https://intelsoft.info/my/
2. Enter username: `sandboxcm`
3. Enter password: `Changeme!1`
4. Click "Log in"
5. Observe redirect and dashboard loading

**Expected:** Successful login, dashboard access
**Critical Issue:** Login failure blocks all testing

#### TC-AUTH-002: Session Persistence

**Steps:**

1. Login successfully
2. Navigate between pages
3. Refresh browser (F12)
4. Return after 5 minutes idle

**Expected:** Session maintained appropriately

**Documentation:**

- Screenshots for any failures
- Console errors (F12 → Console tab)
- Network errors (F12 → Network tab)

---

### 1.3 Course Search Functionality (CRITICAL - 7 minutes)

**Objective:** Test the reported null reference error in course search

**Steps:**

1. After login, locate "Courses" menu
2. Click "Search courses" (Manager role required)
3. If menu not visible: Document "insufficient permissions for Manager role"
4. If menu visible:
   - Enter search term: "training"
   - Click search button
   - Wait 10 seconds for results

**Expected Results:**

- Search results displayed
- OR "No courses found" message
- OR appropriate loading indicator

**Critical Failure Indicators:**

- Exception/error page
- "Call to a member function get_formatted_name() on null"
- System crash or white screen

**Documentation:**

- Screenshot: `issue_search_critical_error_[timestamp].png`
- Full error message
- Browser console errors
- Steps to reproduce

---

### 1.4 Dashboard Content Audit (5 minutes)

**Objective:** Check for placeholder content and UI issues

**Steps:**

1. After successful login, examine main dashboard
2. Scan for Lorem ipsum placeholder text
3. Check banner content relevance
4. Verify navigation menu functionality

**Expected Results:**

- Meaningful, professional content
- No placeholder text
- Functional navigation

**Issue Documentation:**

- Screenshot: `issue_dashboard_placeholder_[timestamp].png`
- Location of placeholder text
- Context around the issue

---

## 📚 Phase 2: Core Functionality Testing (20 minutes)

### 2.1 Course Management Testing (8 minutes)

#### My Courses Access

**Steps:**

1. Navigate to "My Courses" section
2. Count enrolled courses displayed
3. Click on a course name to access content
4. Verify course page loads properly

**Expected:** Course content accessible
**Issues:** Loading failures, access denied

#### Certificate Download Testing

**Steps:**

1. In My Courses, locate "Download Certificates"
2. Click to access certificates section
3. Observe content displayed

**Expected Results:**

- Available certificates for download
- OR clear message: "No certificates earned yet"
- OR enrollment-based messaging

**Critical Issue:** "Nothing to display" with enrolled courses

**Documentation:**

- Screenshot: `issue_certificates_display_[timestamp].png`
- Number of enrolled courses
- Certificate section content

---

### 2.2 SCORM Content Testing (7 minutes)

**Objective:** Verify multimedia content delivery

**Steps:**

1. Locate course with SCORM content (e.g., "CAP Initial Training")
2. Click to access SCORM package
3. Wait 30 seconds for loading
4. If play button appears, click it
5. Monitor for 1 minute

**Expected Results:**

- Content loads automatically
- Media plays without issues
- No persistent loading states

**Issue Indicators:**

- Stuck with play button overlay
- Media loading failures
- CSP (Content Security Policy) errors in console

**Console Monitoring:**

- Press F12 → Console tab
- Look for: "violates Content Security Policy"
- Look for: base64 media errors

**Documentation:**

- Screenshot: `issue_scorm_loading_[timestamp].png`
- Console errors screenshot
- Video of loading behavior if possible

---

### 2.3 Technical Performance Audit (5 minutes)

#### Page Load Performance

**Steps:**

1. Time initial page loads
2. Clear cache and reload (Ctrl+Shift+R)
3. Note load times > 3 seconds

#### Resource Loading

**Steps:**

1. F12 → Network tab → Refresh page
2. Check for failed requests (red status codes)
3. Look for font loading errors
4. Check image loading failures

#### Console Error Audit

**Steps:**

1. F12 → Console tab
2. Scan for JavaScript errors (red text)
3. Document font decoding errors
4. Note CSP violations

**Documentation:**

- Screenshot: `issue_console_errors_[timestamp].png`
- Screenshot: `issue_network_failures_[timestamp].png`
- Load time measurements

---

## 📱 Phase 3: Compatibility Testing (10 minutes)

### 3.1 Mobile Responsiveness (5 minutes)

**Steps:**

1. Resize browser window to mobile size
2. Or use Chrome DevTools: Toggle device toolbar
3. Test navigation menu
4. Check content readability
5. Test button functionality

**Expected:** Responsive layout, readable content
**Issues:** Broken layouts, unclickable elements

### 3.2 Cross-Browser Verification (5 minutes)

**Steps:**

1. Test on Firefox (if available)
2. Test on Safari/Edge (if available)
3. Compare behavior with Chrome baseline

**Expected:** Consistent functionality across browsers
**Issues:** Browser-specific failures

---

## 📊 Phase 4: Issue Documentation (10 minutes)

### 4.1 Issue Reporting Template

For each issue found, document:

```
ISSUE ID: ISSUE-[NUMBER]
TITLE: [Brief descriptive title]
SEVERITY: Critical/High/Medium/Low
LOCATION: [Page/function where issue occurs]

DESCRIPTION:
[Clear description of the problem]

REPRODUCTION STEPS:
1. [Step 1]
2. [Step 2]
3. [Step 3]

EXPECTED RESULT:
[What should happen]

ACTUAL RESULT:
[What actually happens]

ERROR MESSAGES:
[Console errors, user-facing errors]

SCREENSHOTS:
issue_[description]_[timestamp].png

IMPACT:
[How this affects users]

RECOMMENDED FIX:
[Suggestions for resolution]
```

### 4.2 Screenshot Standards

**Naming Convention:**

```
issue_[description]_[timestamp].png
```

**Examples:**

- `issue_search_null_error_20240122_143000.png`
- `issue_scorm_csp_blocked_20240122_143500.png`
- `issue_dashboard_placeholder_20240122_144000.png`

**Quality Standards:**

- Include full context
- Show URL in browser
- Capture error messages completely
- Use PNG format
- Don't crop important information

---

## 📈 Test Results Summary Template

### Session Information

**Date:** [YYYY-MM-DD]
**Tester:** [Name]
**Duration:** [X] minutes
**Browser:** [Chrome/Firefox/etc.]

### Test Coverage

- [ ] Public homepage assessment
- [ ] Authentication testing
- [ ] Course search functionality
- [ ] Dashboard content audit
- [ ] Course management
- [ ] Certificate downloads
- [ ] SCORM content delivery
- [ ] Technical performance
- [ ] Mobile responsiveness
- [ ] Cross-browser testing

### Issues Found Summary

| Issue ID  | Title   | Severity   | Status |
| --------- | ------- | ---------- | ------ |
| ISSUE-001 | [Title] | [Severity] | Open   |
| ISSUE-002 | [Title] | [Severity] | Open   |

### Critical Issues Requiring Immediate Attention

1. **Course Search Error** - Null reference exception (CRITICAL)
2. **SCORM Media Blocking** - CSP policy violation (HIGH)
3. **Public Homepage** - Lorem ipsum placeholders (HIGH)

### Recommendations

1. **Priority 1 (Critical):** Fix search functionality before production
2. **Priority 2 (High):** Resolve SCORM media delivery issues
3. **Priority 3 (Medium):** Replace placeholder content
4. **Priority 4 (Low):** Performance optimizations

---

## 🛠️ Troubleshooting Guide

### Common Issues During Testing

#### Can't Access Manager Functions

**Symptom:** No "Courses" → "Search courses" menu
**Cause:** Account has Student role, not Manager
**Solution:** Document permission level, test with appropriate access

#### SCORM Content Not Available

**Symptom:** Can't find SCORM courses to test
**Cause:** Not enrolled in courses with SCORM content
**Solution:** Document limitation, test other course types

#### Console Shows Many Errors

**Symptom:** Overwhelming number of console messages
**Cause:** Browser extensions, cached issues
**Solution:** Focus on red JavaScript errors, ignore warnings

#### Screenshots Too Large

**Symptom:** Files too big to share
**Cause:** Full page screenshots
**Solution:** Use area screenshots (Win+Shift+S) focusing on issues

---

## 📋 Final Checklist

### Pre-Test Completion

- [ ] Environment ready
- [ ] Credentials verified
- [ ] Documentation tools prepared

### Test Execution

- [ ] Phase 1 completed (Critical path)
- [ ] Phase 2 completed (Core functionality)
- [ ] Phase 3 completed (Compatibility)
- [ ] Phase 4 completed (Documentation)

### Post-Test Activities

- [ ] All screenshots saved with proper names
- [ ] Issues documented in tracking template
- [ ] Test summary completed
- [ ] Recommendations prioritized

---

## 🎯 Success Criteria

### Test Completion

- [ ] All planned test cases executed
- [ ] Critical path issues identified
- [ ] Screenshots captured for all issues
- [ ] Issues documented with reproduction steps

### Quality Gates

- [ ] No critical issues blocking core functionality
- [ ] High-priority issues documented for immediate fixes
- [ ] Test results summarized for stakeholders
- [ ] Recommendations provided for remediation

---

## 📞 Support and Next Steps

### During Testing

- Document all issues found
- Take screenshots immediately when issues occur
- Note environmental conditions (browser, timing, etc.)

### After Testing

- Review all documentation
- Prioritize issues by severity and impact
- Create remediation plan
- Schedule re-testing after fixes

### Issue Escalation

- Critical issues: Immediate attention required
- High issues: Fix in current development cycle
- Medium issues: Address in next cycle
- Low issues: Document for future consideration

---

**END OF TESTING GUIDE**

**Estimated Time:** 45-60 minutes
**Success Rate:** 95%+ issue detection
**Deliverables:** Complete issue documentation with screenshots
