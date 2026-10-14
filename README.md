# Topic-3-assesment
My assessment tasks and documentation# Topic 3: Core Nodes & Data Mapping

## 1. Overview

This project demonstrates a beginner-level n8n workflow using the Manual Trigger and Edit Fields (Set) nodes. It creates a product record, modifies an existing Boolean value, dynamically maps data using n8n expressions, and calculates a product price including 10% tax.

## 2. Objective

- Create String, Number, and Boolean fields.
- Modify an existing field while preserving incoming data.
- Use dynamic expressions for data mapping.
- Calculate a value using an expression.
- Execute and validate the final JSON output.

## 3. Workflow Structure

The workflow consists of three connected nodes:

1. **Manual Trigger** – Starts the workflow when executed manually.
2. **Set Original Data** – Creates the initial product record.
3. **Modify & Map** – Updates product availability, maps the product name, and calculates the price including tax.

**Workflow sequence:**

`Manual Trigger → Set Original Data → Modify & Map`

## 4. Initial Product Data

The `Set Original Data` node creates these fields:

| Field | Type | Value |
|---|---|---|
| `productName` | String | `Wireless Mouse` |
| `basePrice` | Number | `25` |
| `isAvailable` | Boolean | `true` |

## 5. Data Mapping and Expressions

The `Modify & Map` node performs the following operations:

### Update availability

- Field: `isAvailable`
- Type: Boolean
- New value: `false`

### Dynamically map the product name

- Field: `inventoryLabel`
- Type: String
- Expression:

`{{ $json.productName }}`

This expression retrieves the incoming `productName` value instead of using a hardcoded label.

### Calculate the price including tax

- Field: `priceWithTax`
- Type: Number
- Expression:

`{{ $json.basePrice * 1.1 }}`

This calculates the original price plus 10% tax.

Calculation:

- Base price = 25
- Tax = 25 × 10% = 2.5
- Final price = 25 + 2.5 = 27.5

## 6. Expected Final JSON Output

After successful execution, the workflow should produce the following data structure:

```json
{
  "productName": "Wireless Mouse",
  "basePrice": 25,
  "isAvailable": false,
  "inventoryLabel": "Wireless Mouse",
  "priceWithTax": 27.5
}
```

Note: Floating-point calculations may display a value such as `27.500000000000004`. This is a normal numerical precision artifact. The calculated result is effectively 27.5.

## 7. Setup and Execution Instructions

1. Open your n8n workspace.
2. Import `topic3_core_nodes_workflow.json` if setting up the workflow in another workspace.
3. Verify that the three nodes are connected in the correct order.
4. Open `Set Original Data` and confirm the field names, types, and values.
5. Open `Modify & Map` and verify the Boolean value and both expressions.
6. Ensure **Include Other Input Fields** is enabled so the original product fields are retained.
7. Click **Execute workflow**.
8. Inspect the final JSON output and confirm that all five required fields are present.
9. Save and export the completed workflow.

## 8. Validation Checklist

- [x] Workflow contains a Manual Trigger node.
- [x] Initial product data is configured.
- [x] String, Number, and Boolean data types are used.
- [x] Availability is updated from `true` to `false`.
- [x] Product name is mapped dynamically.
- [x] Price including 10% tax is calculated.
- [x] Original input fields are preserved.
- [x] Final output contains all five required fields.
- [x] Workflow executes successfully.

## 9. Repository Contents

The GitHub repository should contain:

- `topic3_core_nodes_workflow.json` – Exported n8n workflow.
- `README.md` – Workflow documentation and execution instructions.
- `screenshots/` – Supporting screenshots of the workflow, node configurations, and execution output.

## 10. Assessment Deliverables

- Public GitHub repository containing the workflow JSON and README.
- Screenshots demonstrating node configurations and successful execution.
- Loom or YouTube demonstration video showing the workflow, expressions, execution, and final JSON output.

## 11. Challenges and Observations

The workflow uses dynamic expressions to map incoming data and calculate the price including tax. The original input fields must be preserved when configuring the second Edit Fields node.

Floating-point precision may cause the calculated price to display additional decimal digits. The result is mathematically equivalent to 27.5.

## 12. Conclusion

This assessment demonstrates the use of core n8n nodes, typed data fields, Boolean modification, dynamic data mapping, mathematical expressions, and output validation. The completed workflow provides a practical example of transforming product data in an automated workflow.

