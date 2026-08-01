---
name: Quote carrier services and create a shipment
description: Compare Packlink PRO carrier services for a parcel and create a shipment with a printable label.
api: openapi/packlink-openapi.yml
operations: [searchServices, getServiceDetails, createShipment, getShipmentLabels]
---

# Quote carrier services and create a shipment (Packlink PRO)

Use this skill to price carrier options for a parcel and book a shipment.

## Auth
All calls require the Packlink PRO API key in the `Authorization` header
(see `authentication/packlink-authentication.yml`). Base URL: `https://api.packlink.com`.

## Steps
1. **Search services** — call `searchServices` (`POST /v1/services`) with the origin,
   destination, and parcel dimensions/weight to get available carrier services and prices.
2. **Inspect a service** — call `getServiceDetails`
   (`GET /v1/services/available/{id}/details`) for the chosen service `id` to confirm
   drop-off/pickup requirements and constraints.
3. **Create the shipment** — call `createShipment` (`POST /v1/shipments`) referencing the
   chosen service; capture the returned shipment `reference`.
4. **Get the label** — call `getShipmentLabels` (`GET /v1/shipments/{reference}/labels`)
   to retrieve the printable label URL(s).

## Notes
- No idempotency-key header is documented; avoid blind retries on `createShipment`
  (see `conventions/packlink-conventions.yml`).
- Errors: `400` = bad/missing parameters, `401` = bad API key
  (see `errors/packlink-problem-types.yml`).
