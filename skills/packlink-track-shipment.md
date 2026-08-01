---
name: Track a shipment and sync status
description: Retrieve tracking events for a Packlink PRO shipment and register a webhook to stay in sync.
api: openapi/packlink-openapi.yml
operations: [getShipment, trackShipment, registerShipmentCallback]
---

# Track a shipment and sync status (Packlink PRO)

Use this skill to read a shipment's tracking history and keep an integration in sync.

## Auth
All calls require the Packlink PRO API key in the `Authorization` header. Base URL:
`https://api.packlink.com`.

## Steps
1. **Load the shipment** — call `getShipment` (`GET /v1/shipments/{reference}`) to confirm
   the shipment exists and read its current state.
2. **Read tracking events** — call `trackShipment`
   (`GET /v1/shipments/{reference}/track`) for the carrier tracking timeline.
3. **Register a webhook (optional)** — call `registerShipmentCallback`
   (`POST /v1/shipments/callback`) with a callback URL so Packlink pushes shipment
   status changes instead of you polling
   (see `asyncapi/packlink-webhooks.yml`).

## Notes
- `404` means the `reference` is unknown; `401` means the API key is missing/invalid
  (see `errors/packlink-problem-types.yml`).
