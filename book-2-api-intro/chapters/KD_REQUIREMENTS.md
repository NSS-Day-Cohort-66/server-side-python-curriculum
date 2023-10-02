# Kneel Diamonds Feature Requirements

No surprise, your Kneel Diamonds API must support all of the basic CRUD operations.

- POST an **Order**
- GET a single **Order**
- GET a list of **Order**
- PUT an **Order**
- DELETE an **Order**

A client can't access metals, styles, and sizes since those are managed internally by the Kneel Diamonds staff. That data is used during the management of orders.

## Support Expanding Orders

Once you implement all of the basic CRUD operations, you need to support expanding any of the related resources on an order.

GET http://localhost:8000/orders/1?_expand=metal

```json
{
    "id": 1,
    "metal_id": 3,
    "style_id": 1,
    "caret_id": 2,
    "metal": {
        "id": 3,
        "metal": "24K Gold",
        "price": 1258.9
    }
}
```

GET http://localhost:8000/orders/1?_expand=caret

```json
{
    "id": 1,
    "metal_id": 3,
    "style_id": 1,
    "caret_id": 2,
    "caret": {
        "id": 2,
        "carets": 0.75,
        "price": 782
    }
}
```
