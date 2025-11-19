# Cortex Cloud APIs - Update Changelog (IAM APIs Added)

## 🎉 Update Complete!

**Date:** 2025-11-10  
**From:** 223 endpoints → **To:** 238 endpoints  
**Added:** 15 new IAM endpoints  
**Version:** Cortex Cloud Platform APIs v1.3

---

## 📊 Summary

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| **Total Endpoints** | 223 | 238 | **+15** |
| **API Categories** | 8 | 9 | +1 (IAM) |
| **IAM Endpoints** | 0 | 15 | **+15 NEW** |

---

## ✅ What Was Added

### 🆕 Identity and Access Management (IAM) APIs

A complete new category with 15 endpoints across 5 functional areas:

#### 1. **Roles** (4 endpoints)
Manage IAM roles and permissions.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/platform/iam/v1/role` | Get list of roles |
| POST | `/platform/iam/v1/role` | Create a new role with component & dataset permissions |
| DELETE | `/platform/iam/v1/role/{role_id}` | Delete an existing role |
| GET | `/platform/iam/v1/role/permission-config` | Get available permissions for tenant |

**Key Features:**
- Component permissions management
- Dataset permissions management
- Permission configuration discovery

**Example - Create Role:**
```json
POST /platform/iam/v1/role
{
  "request_data": {
    "component_permissions": ["rules_action", "wf_verdict_change"],
    "dataset_permissions": [{
      "dataset_group_name": "xdr_data",
      "permissions": ["xdr_data"]
    }],
    "description": "Security Analyst Role",
    "pretty_name": "security_analyst"
  }
}
```

---

#### 2. **User Groups** (4 endpoints)
Manage user groups for organized access control.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/platform/iam/v1/user-group` | Get list of user groups |
| POST | `/platform/iam/v1/user-group` | Create a new user group |
| PATCH | `/platform/iam/v1/user-group/{group_id}` | Update user group details |
| DELETE | `/platform/iam/v1/user-group/{group_id}` | Delete user group |

**Key Features:**
- Hierarchical group management
- Role assignment to groups
- Group-based access control

**Example - Create User Group:**
```json
POST /platform/iam/v1/user-group
{
  "request_data": {
    "group_name": "security_team",
    "role_id": "security_analyst",
    "description": "Security Operations Team"
  }
}
```

---

#### 3. **Users** (3 endpoints)
Manage individual users and their properties.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/platform/iam/v1/user` | Get list of all users |
| GET | `/platform/iam/v1/user/{user_email}` | Get user by email address |
| PATCH | `/platform/iam/v1/user/{user_email}` | Update user details |

**Key Features:**
- User profile management
- Status management (Active/Inactive)
- Role assignment
- Phone number updates

**Example - Update User:**
```json
PATCH /platform/iam/v1/user/john.doe@company.com
{
  "request_data": {
    "phone_number": "408-753-4000",
    "status": "Active",
    "role_id": "security_analyst",
    "scope_entity_id": "team_alpha"
  }
}
```

---

#### 4. **Scopes** (2 endpoints)
Manage entity-level access scopes.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/platform/iam/v1/scope/{entity_type}/{entity_id}` | Get scope details |
| PUT | `/platform/iam/v1/scope/{entity_type}/{entity_id}` | Update scope configuration |

**Key Features:**
- Endpoint group scoping
- Endpoint filter management
- Entity-level access control

**Example - Update Scope:**
```json
PUT /platform/iam/v1/scope/user_group/team_alpha
{
  "request_data": {
    "endpoints": {
      "endpoint_groups": {
        "names": ["production-servers"],
        "mode": "scope"
      },
      "endpoint_filters": {
        "filters": [],
        "mode": "scope"
      }
    }
  }
}
```

---

#### 5. **API Keys** (2 endpoints)
Programmatic API key management.

| Method | Endpoint | Description |
|--------|----------|-------------|
| GET | `/platform/iam/v1/api-key/{api_key_id}` | Get API key details |
| PUT | `/platform/iam/v1/api-key/{api_key_id}` | Update API key configuration |

**Key Features:**
- Role assignment to API keys
- Security level management
- Key metadata updates

**Example - Update API Key:**
```json
PUT /platform/iam/v1/api-key/123
{
  "request_data": {
    "roles": ["security_analyst", "incident_responder"],
    "security_level": "standard",
    "comment": "Updated for Q4 2025"
  }
}
```

---

## 🔑 Authentication Changes

### New Base URL for IAM APIs

**IAM APIs use a different base path:**
```
https://{fqdn}/platform/iam/v1/
```

**Standard Cortex APIs continue to use:**
```
https://api-{fqdn}/public_api/
```

### Authentication Headers

**For public_api endpoints:**
```
x-xdr-auth-id: {api_key_id}
Authorization: {api_key}
Content-Type: application/json
```

**For platform IAM endpoints:**
```
Content-Type: application/json
(Authentication handled via session/token)
```

---

## 📁 Updated Collection Structure

```
Cortex Cloud APIs (238 endpoints)
│
├── ASPM, CICD and Application Security APIs (50 endpoints)
│   ├── Applications (6)
│   ├── Criteria (4)
│   ├── Integrations (4)
│   ├── Labels (1)
│   ├── Operational risk (1)
│   ├── Policies (5)
│   ├── Remediations (3)
│   ├── Repositories (4)
│   ├── Repository branches (2)
│   ├── Rules (7)
│   ├── SBOM management (2)
│   └── Scan management (7)
│
├── Cloud Onboarding APIs (14 endpoints)
│   ├── General (2)
│   ├── Cloud account management (2)
│   ├── Cloud Integration Instance management (7)
│   └── Outpost management (3)
│
├── Compliance Controls API (27 endpoints)
│   ├── Assessment profiles (5)
│   ├── Assessment results (1)
│   ├── Compliance Assets (1) **NEW v1.3**
│   ├── Categories (1)
│   ├── Controls (6)
│   ├── Reports (1)
│   ├── Results (2)
│   ├── Rules (2)
│   └── Standards (6)
│
├── Cortex Cloud Platform APIs (XX endpoints)
│   ├── API keys (3)
│   ├── Alerts (2)
│   ├── Asset groups (5)
│   ├── Asset inventory (5)
│   ├── Attack surface management (4)
│   ├── Audit log (2)
│   ├── Authentication settings (5)
│   ├── BIOCs (3)
│   ├── Cases (2)
│   ├── Identity and Access Management (IAM) (15) **NEW** ⭐
│   │   ├── Roles (4)
│   │   ├── User Groups (4)
│   │   ├── Users (3)
│   │   ├── Scopes (2)
│   │   └── API Keys (2)
│   └── [Other sections...]
│
├── Cloud CIEM APIs
├── Cloud Workload Protection APIs
└── Vulnerability Management APIs
```

---

## 🎯 Use Cases for IAM APIs

### 1. **Automated User Provisioning**
```python
# Create role
role = create_role("security_analyst", permissions=[...])

# Create user group
group = create_user_group("security_team", role_id=role['id'])

# Update user with role
update_user("new.hire@company.com", role_id=role['id'])
```

### 2. **Role-Based Access Control (RBAC)**
```python
# Get available permissions
perms = get_permission_config()

# Create custom role with specific permissions
role = create_role(
    name="custom_analyst",
    component_permissions=["rules_action", "alerts_view"],
    dataset_permissions=[...]
)
```

### 3. **API Key Management**
```python
# Get API key details
key_info = get_api_key(api_key_id)

# Update API key roles
update_api_key(
    api_key_id,
    roles=["security_analyst", "incident_responder"],
    security_level="advanced"
)
```

### 4. **Scope Management**
```python
# Set endpoint scope for user group
update_scope(
    entity_type="user_group",
    entity_id="team_alpha",
    endpoint_groups=["production-servers"]
)
```

### 5. **Bulk User Management**
```python
# Get all users
users = get_users()

# Update multiple users
for user in users:
    if user['department'] == 'security':
        update_user(
            user['email'],
            role_id="security_analyst",
            status="Active"
        )
```

---

## 📋 Files Updated

### 1. **Postman Collection**
**File:** `Cortex_Cloud_APIs_FINAL.json`
- ✅ Added IAM folder with 5 subfolders
- ✅ Added 15 new endpoints with complete schemas
- ✅ Total: 238 endpoints

### 2. **Compact llms.txt**
**File:** `llms.txt` (22KB)
- ✅ Added IAM section overview
- ✅ Listed all 15 new endpoints
- ✅ Updated total count to 238

### 3. **Complete llms.txt**
**File:** `llms-complete.txt` (1.2MB)
- ✅ Added complete IAM endpoint details
- ✅ Full request/response schemas
- ✅ All headers and parameters
- ✅ Complete examples for each endpoint

---

## 🚀 Quick Start with IAM APIs

### Import Updated Collection
```
1. Open Postman
2. Import: Cortex_Cloud_APIs_FINAL.json
3. Navigate to: Cortex Cloud Platform APIs > IAM
4. Configure your {{fqdn}} variable
```

### Test IAM Endpoints
```
1. GET /platform/iam/v1/role - List all roles
2. GET /platform/iam/v1/user - List all users
3. GET /platform/iam/v1/user-group - List all groups
```

### Use with AI
```
Upload llms-complete.txt and ask:
"Generate Python code to manage IAM roles with the Cortex Cloud API"
```

---

## 🔄 Migration Notes

### No Breaking Changes
- ✅ All existing endpoints remain unchanged
- ✅ No deprecated endpoints
- ✅ Backwards compatible

### New Capabilities Added
- ✅ Programmatic IAM management
- ✅ Role-based access control automation
- ✅ User lifecycle management
- ✅ API key management

### Authentication
- ✅ IAM endpoints may use different auth
- ✅ Check documentation for specific requirements
- ✅ Standard Cortex auth works for most endpoints

---

## 📖 Documentation References

### Official Sources
- **PDF:** Cortex Cloud Platform APIs v1.3 (598 pages)
- **IAM Section:** Pages 339-362
- **What's New:** Page 9

### API Explorer
- **IAM Roles:** `/platform/iam/v1/role`
- **IAM Users:** `/platform/iam/v1/user`
- **IAM Groups:** `/platform/iam/v1/user-group`

---

## ✅ Verification Checklist

Before using the updated collection:

- [ ] Import updated collection into Postman
- [ ] Verify IAM folder exists (15 endpoints across 5 subfolders)
- [ ] Configure {{fqdn}} environment variable
- [ ] Test GET /platform/iam/v1/role endpoint
- [ ] Review IAM authentication requirements
- [ ] Update any automation scripts if needed
- [ ] Review new use cases for your organization
- [ ] Test role creation with your permissions
- [ ] Verify user management capabilities
- [ ] Check API key management features

---

## 📊 Complete Statistics

### Before Update
- Total Endpoints: 223
- API Categories: 8
- IAM Endpoints: 0

### After Update
- Total Endpoints: 238 (+15)
- API Categories: 9 (+1)
- IAM Endpoints: 15 (NEW)

### Breakdown by Category
1. ASPM APIs: 50 endpoints
2. **IAM APIs: 15 endpoints** ⭐ NEW
3. Compliance: 27 endpoints
4. Cloud Onboarding: 14 endpoints
5. Other categories: 132 endpoints

---

## 🎉 Summary

**What You Get:**
- ✅ 15 new IAM endpoints for identity management
- ✅ Complete role-based access control (RBAC)
- ✅ User and group management automation
- ✅ API key lifecycle management
- ✅ Scope and permission management
- ✅ Updated Postman collection (238 endpoints)
- ✅ Updated llms.txt files (both versions)
- ✅ Full documentation and examples

**Ready to Use:**
- Import collection → Configure → Test → Automate!

---

**Last Updated:** 2025-11-10  
**Version:** Cortex Cloud Platform APIs v1.3  
**Status:** ✅ Complete and Ready  
**Total Endpoints:** 238 (was 223, +15 IAM endpoints)
