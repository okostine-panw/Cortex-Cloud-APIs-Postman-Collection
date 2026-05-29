# Postman Collection Update Summary

## Date: May 29, 2026
## Collection: Cortex Cloud APIs 2.1

---

## Overview

The Postman collection has been updated to reflect the latest Cortex Cloud API changes for Issues and Cases endpoints. All endpoint descriptions now include documentation for new fields and API changes.

---

## Updates Applied

### ✅ Issues API (7 requests + 1 new endpoint)

**Updated Requests:**
1. ✓ Create a new issue
2. ✓ Retrieve issues based on filters
3. ✓ Retrieve issues based on filters Copy
4. ✓ Retrieve issues based on filters Copy 2
5. ✓ Retrieve issues context
6. ✓ Retrieve issues context Copy
7. ✓ Update existing issue

**New Endpoint Added:**
8. ✓ Get issue schema - `POST /public_api/v1/issue/schema/`

### ✅ Cases API (6 requests updated)

**Updated Requests:**
1. ✓ Retrieve cases based on filters
2. ✓ Retrieve cases based on filters Copy
3. ✓ Retrieve incidents instead of cases
4. ✓ Get War Room entries
5. ✓ Add War Room entries
6. ✓ Update existing case

---

## New Fields Documented

### Issues API - 11 New Fields

Each Issues endpoint now documents these new fields:

| Field | Type | Description |
|-------|------|-------------|
| `action_status` | string | Action status tracking |
| `agentic_assistant_id` | string | AI assistant identifier |
| `agentic_response_conversation_id` | string | AI conversation tracking |
| `agentic_response_status` | string | AI response status |
| `asset_cloud_account_names` | array | Cloud account names |
| `asset_external_provider_ids` | array | External provider IDs |
| `case_ids` | array | Linked case IDs (bidirectional) |
| `exception_expiration` | timestamp | Exception expiration date |
| `exception_ids` | array | Exception identifiers |
| `initial_evidence` | string | Initial evidence data |
| `is_excepted` | boolean | Exception status flag |

### Response Wrapper Changes

All Issues endpoints now document the response wrapper changes:
- ~~`issues`~~ → `DATA`
- ~~`total_count`~~ → `TOTAL_COUNT`
- ~~`result_count`~~ → `FILTER_COUNT`

---


## How to Use the Updated Collection

### 1. Import into Postman

**Option A: Re-import (Recommended)**
1. Open Postman
2. Click **Import** button
3. Select the updated `Cortex Cloud APIs 2.1.postman_collection.json`
4. Choose **Replace** when prompted

### 2. Review Updated Descriptions

1. Navigate to **Cortex Cloud Platform APIs** folder
2. Open **Issues** or **Cases** subfolder
3. Click any request
4. View the **Description** tab to see new field documentation

---

## Example Queries Using New Fields

### 1. Find Issues with Exceptions

```json
{
  "request_data": {
    "filters": [
      {
        "field": "is_excepted",
        "operator": "eq",
        "value": true
      }
    ],
    "search_from": 0,
    "search_to": 100
  }
}
```

### 2. Find Issues Linked to Specific Case

```json
{
  "request_data": {
    "filters": [
      {
        "field": "case_ids",
        "operator": "contains",
        "value": "case-12345"
      }
    ],
    "search_from": 0,
    "search_to": 100
  }
}
```

### 3. Find Issues with AI Assistant Responses

```json
{
  "request_data": {
    "filters": [
      {
        "field": "agentic_assistant_id",
        "operator": "neq",
        "value": null
      }
    ],
    "search_from": 0,
    "search_to": 100
  }
}
```

---
