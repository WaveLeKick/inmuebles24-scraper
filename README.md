[Inmuebles24 Scraper](https://apify.com/juandiaz.mx/inmuebles24-scraper?fpr=data)

# Inmuebles24 Scraper Pro 🏠

Professional and high-performance real estate scraper for [Inmuebles24](https://www.inmuebles24.com), the leading real estate portal in Mexico.

## 🚀 Key Features

- **Anti-Bot Bypass**: Advanced header management and residential proxy support to ensure high success rates.
- **Detailed Metadata**: Extracts not just titles and prices, but also full descriptions, features (rooms, bathrooms, size), and coordinates.
- **Smart Filters**: Search by location, property category, and transaction type.
- **Price Alerts**: Built-in support for identifying price drops based on a configurable percentage threshold.
- **Agent-Ready**: Fully compatible with AI agents and automation workflows via structured JSON output.

## 📥 Input Parameters

The actor accepts the following configuration:

| Field | Type | Description |
| --- | --- | --- |
| `city` | String | (Required) The city or location to search. |
| `propertyType` | String | Category: Casas, Departamentos, Terrenos, etc. |
| `transactionType` | String | Operation: Venta, Renta, Temporal. |
| `maxItems` | Number | Maximum number of results to fetch. |
| `proxyConfiguration` | Object | Connection settings (Residential recommended). |

## 📤 Output Example

Data is delivered in clean JSON format:

```
{
  "title": "Departamento de Lujo en Polanco",
  "price": 12500000,
  "currency": "MXN",
  "location": "Polanco, Miguel Hidalgo, CDMX",
  "latitude": 19.4326,
  "longitude": -99.1332,
  "propertyType": "Departamento",
  "url": "https://www.inmuebles24.com/propiedades/polanco-lujo-..."
}
```

## 🛡️ Best Practices

For optimal results and to avoid being blocked by Inmuebles24 protection systems, we recommend:

1. Using **Apify Residential Proxies** (specifically from Mexico).
2. Limiting your searches to reasonable volumes (e.g., 200-500 items per run).
3. Providing specific city names in the `city` field.

## ⚖️ Pricing & Monetization

This Actor follows the **Pay per result** model. You only pay for successful extractions, making it cost-effective for both small and large scale operations.

---

*Developed by Juan Diaz - Expert Real Estate Data Solutions.*