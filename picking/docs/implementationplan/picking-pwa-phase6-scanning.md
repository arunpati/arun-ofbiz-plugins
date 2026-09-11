# Picking PWA - Phase 6: Scanning & Recording

This phase implements the high-performance picking interface with scanning support.

## Proposed Changes

### [Frontend] Picking Interface
#### [NEW] [PickingDetail.jsx](file:///Users/arun/personal/arun/ofbiz_dev/picking-app/src/screens/PickingDetail.jsx)
- Interactive view for the current target item.
- Visual display of: Location (Aisle, Section, Level), Product Name, SKU/Product ID, and Quantity to pick.
- Navigation controls to skip items or manually confirm picks.
- Integrated into the flow via `ActivePicklist.jsx` (either as a toggleable detailed view or a dedicated route/sub-route like `/picklist/:picklistId/pick`).

### [Frontend] Scanning Integration
#### [NEW] [ScannerManager.js](file:///Users/arun/personal/arun/ofbiz_dev/picking-app/src/utils/ScannerManager.js)
- **Camera Scan**: Wrapper for `html5-qrcode` to enable camera-based scanning. (Note: `html5-qrcode` must be added to `package.json` dependencies).
- **Hardware Scan**: Global `keydown` listener to capture input from Bluetooth/HID scanners.
- Automatic focus management to ensure scanning works without manual tap.

### [Integration] Pick Recording
Implement the link to the `POST /rest/services/setPicklistItemToComplete` API (exposed via the `recordPick` method in `usePickingApi.js`) to update the backend as items are scanned or manually confirmed.
- Handle optimistic UI updates for a "fast feel".

## Verification Plan

### Manual Verification
- Test camera scanning with a mock QR code/Barcode on a smartphone.
- Simulate hardware scanning by typing a SKU into the browser while the listener is active.
- Verify status changes in the UI after a successful scan.

