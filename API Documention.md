# Create a basic API for a given class

Create a simple REST API for a Product class and document it.

---

## Selected API Endpoint

This provides an API for a product, which is the same as the one for the product in Java but is an equivalent REST style API.

---

# 1. This is the output of the Endpoint Documentation (Prompt 1).

## GET /api/products

### Description
Returns a list of products, filtering, sorting and paged (optional).

---

### Query Parameters

Category (String): filter by product category.  
A double that is used to filter on a minimum price.A double used to filter by its minimum price.  
The maximum price filter (Double) – the maximum price for the item being filtered for.  
The field to sort by (default: createdAt) – this could be a string.  
The direction of the sorting.The direction in which the sorting is done. (asc or desc – String)  
A page number.Type: int - the page number.  
Enables showing only a limited number of results per page.- limit (int) – Number of results per page  
- `InStock Only` (boolean) – Only return products that are in stock.

---

### Responses

#### 200 OK
Gets product list, paginates.Returns product list (paginated)

```json
{
  "products": [],
  "pagination": {
    "total": 0,
    "page": 1,
    "limit": 20,
    "pages": 0
  }
}
