[Inmuebles24 Scraper](https://apify.com/fatihtahta/inmuebles24-scraper?fpr=data)

# Inmuebles24 Scraper

**Slug:** `fatihtahta/inmuebles24-scraper`

## Overview

Inmuebles24 Scraper collects structured real estate listing records from [Inmuebles24](https://www.inmuebles24.com), including listing identity, title, description, price, location, property type, seller information, publication details, media availability, and source URLs. Inmuebles24 is one of Mexico's major real estate marketplaces, making its public listing data useful for understanding supply, pricing, geography, and inventory movement across local property markets. The actor turns repeatable searches into normalized JSON records that can be used in analytics, enrichment, monitoring, and operational reporting workflows. It is designed for consistent recurring data acquisition, so teams can run the same collection scope over time and compare results without manually rebuilding datasets. Output is structured for automation and downstream systems while reflecting the public data available at run time.

## Why Use This Actor

- **Market research and analytics teams:** build repeatable market intelligence datasets for pricing, supply, availability, property categories, and geographic coverage.
- **Product and content teams:** populate property discovery experiences, comparison tools, editorial research, or internal catalogs with normalized listing attributes.
- **Developers and data engineering teams:** feed structured extraction results into downstream systems, warehouses, enrichment pipelines, and operational reporting jobs.
- **Lead generation and enrichment teams:** identify public listings, publishers, locations, property characteristics, and contact-ready records for qualification workflows.
- **Monitoring and competitive tracking teams:** schedule recurring data acquisition to observe listing changes, publication recency, price movement, and segment-level inventory shifts.

## Common Use Cases

- **Market intelligence:** monitor supply, pricing, availability, property types, publication recency, locations, and category movement across Mexican real estate markets.
- **Lead generation:** build targeted prospect lists from public property listings, publisher profiles, and direct-owner or agency inventory.
- **Competitive monitoring:** track listing volume, pricing posture, rich-media usage, and new inventory across selected cities, neighborhoods, or seller categories.
- **Catalog and directory building:** populate internal databases with structured public real estate records and source links.
- **Data enrichment:** add current public listing attributes, seller details, media indicators, and location metadata to CRM, BI, or analytics datasets.
- **Recurring reporting:** schedule periodic runs for dashboards, alerts, trend analysis, and operational review.

## Quick Start

1. Choose one or more `location` values to define the geographic scope.
2. Select the relevant `deal_type`, `property_type`, price, area, publication date, or seller filters for your use case.
3. Set a small `limit` for the first validation run.
4. Run the actor in Apify Console.
5. Inspect the first dataset records to confirm the output shape, identifiers, and key fields match your workflow.
6. Increase coverage, broaden or narrow filters, and schedule the actor once the output is verified.

## Input Parameters

Configure the available filters below to define the collection scope.

| Parameter | Type | Description | Default |
| --- | --- | --- | --- |
| `location` | array of strings | One or more Mexican cities, neighborhoods, municipalities, or states to collect from, such as `benito juarez` or `ciudad de mexico`. More specific locations usually produce more focused results. | – |
| `deal_type` | string | Transaction category. Allowed values: `all`, `rent`, `buy`, `foreclosure`, `short_term`, `new_development`, `lease_transfer`. | `all` |
| `sort_by` | string | Result ordering. Allowed values: `most_relevant`, `lowest_price`, `newest`, `highest_price`, `most_viewed`, `price_reduced`, `top_sellers`. | `most_relevant` |
| `seller_type` | string | Limits results by publisher type. Allowed values: `real_estate_agency`, `direct_listing`. Leave empty to include both where available. | – |
| `multimedia` | array of strings | Requires selected media types. Allowed values: `360_tour`, `video`, `floor_plan`. | – |
| `view` | string | Property exposure filter. Allowed values: `front_facing`, `interior_facing`. | – |
| `building_age` | string | Property age or construction stage. Allowed values: `under_construction`, `brand_new`, `up_to_5_years`, `up_to_10_years`, `up_to_20_years`, `up_to_50_years`, `over_50_years`. | – |
| `publication_date` | string | Publication freshness window. Allowed values: `since_yesterday`, `today`, `last_week`, `last_15_days`, `last_30_days`, `last_45_days`. | – |
| `property_type` | array of strings | Property categories to include. Allowed values: `apartment`, `house`, `land_lot`, `condo_house`, `commercial_space`, `commercial_warehouse`, `zoned_property`, `shared_apartment`, `horizontal_development`, `mixed_development`, `vertical_development`, `duplex`, `building`, `orchard`, `urban_income_property`, `mall_retail_unit`, `industrial_warehouse`, `office`, `country_house`, `ranch`, `commercial_land`, `industrial_land`, `villa`. | – |
| `min_bedroom` | string | Minimum bedroom count. Allowed values: `1`, `2`, `3`, `4`, `5`. | – |
| `max_bedroom` | string | Maximum bedroom count. Allowed values: `1`, `2`, `3`, `4`, `5`. | – |
| `min_bathroom` | string | Minimum bathroom count. Allowed values: `1`, `2`, `3`, `4`, `5`. | – |
| `min_parking` | string | Parking requirement. `0` means listings with no parking spaces only; `1`, `2`, `3`, and `4` mean at least that many spaces. | – |
| `min_price` | integer | Minimum listing price. Currency follows the listing data returned by Inmuebles24, commonly Mexican pesos where shown as `MN`. Must be `0` or greater. | – |
| `max_price` | integer | Maximum listing price. Currency follows the listing data returned by Inmuebles24, commonly Mexican pesos where shown as `MN`. Must be `0` or greater. | – |
| `min_building_area` | integer | Minimum built or covered area in square meters. Must be `0` or greater. | – |
| `max_building_area` | integer | Maximum built or covered area in square meters. Must be `0` or greater. | – |
| `min_land_area` | integer | Minimum land or lot area in square meters. Must be `0` or greater. | – |
| `max_land_area` | integer | Maximum land or lot area in square meters. Must be `0` or greater. | – |
| `limit` | integer | Maximum number of listings to save per location. Leave empty to collect all matching listings the actor can reach. Must be `1` or greater. | – |

## Choosing Inputs

Use `location` as the primary scope control, then add filters only when they match a clear business question. Narrower filters such as `deal_type`, `property_type`, `seller_type`, `publication_date`, price range, area range, bedrooms, bathrooms, parking, media requirements, and building age produce more targeted datasets; broader filters improve discovery and make it easier to understand the full market surface. `sort_by` affects which matching listings are prioritized first, which is useful when validating a segment or collecting a limited sample. Start with a small `limit` to confirm output quality, then increase it after checking that the dataset contains the records and fields your workflow needs.

## Example Inputs

### Recently Posted Rental Monitoring

```
{
  "location": ["ciudad de mexico"],
  "deal_type": "rent",
  "property_type": ["apartment"],
  "publication_date": "last_week",
  "sort_by": "newest",
  "limit": 50
}
```

### Targeted Buyer Market Analysis

```
{
  "location": ["benito juarez"],
  "deal_type": "buy",
  "property_type": ["apartment", "condo_house"],
  "min_price": 2500000,
  "max_price": 7000000,
  "min_bedroom": "2",
  "limit": 75
}
```

### Broad Discovery With Rich Media

```
{
  "location": ["queretaro"],
  "deal_type": "all",
  "multimedia": ["video", "floor_plan"],
  "sort_by": "most_relevant",
  "seller_type": "real_estate_agency",
  "limit": 100
}
```

## Output

### Output destination

The actor writes results to an Apify dataset as JSON records. The dataset is designed for direct consumption by analytics tools, ETL pipelines, and downstream APIs without post-processing.

Each item contains a stable record envelope plus a type-specific payload when the output has multiple entity types.

### Record envelope (all items)

All records include the following stable envelope fields:

- **type** *(string, required)*: record type, such as `listing`.
- **id** *(number, required)*: source listing identifier.
- **url** *(string, required)*: canonical public listing URL.

Recommended idempotency key: `type + ":" + id`.

Use this key for deduplication and upserts when syncing records into databases, warehouses, CRMs, or search indexes. The envelope makes records easier to merge, deduplicate, and sync across repeated runs.

### Examples

#### Example: listing (`type = "listing"`)

```
{
  "type": "listing",
  "id": 141933064,
  "url": "https://www.inmuebles24.com/propiedades/desarrollo/ememvein-ri-a-bosques-renta-y-estrena-nuestros-depas.-loft-1-141933064.html",
  "posting_code": "Renta",
  "title": "Riğa Bosques Renta y Estrena Nuestros Depas. (Loft, 1 y 2 Recámaras)",
  "generated_title": "Desarrollo vertical",
  "description": "Renta sin Aval en 24 horas. Proceso ágil y flexible. / Lease without guarantor with agile and flexible processes in 24 hours. Opción de departamentos amueblados por Bo-Concept. / Furnished apartments by Bo-Concept available. Todos los departamentos incluyen electrodomésticos. (microondas, lava-secadora, Refrigerador, estufa con horno, lavavajillas) persianas / canceles. All apartments include appliances. (microwave, washer-dryer, refrigerator, stove with oven, dishwasher) blinds / gates. ! estrena depa en la Torre mas emblemática de la cdmx! Brand new apartments just released to the market in the most iconic tower in cdmx. Departamentos tipo: Loft, 1 y 2 recámaras; a un minuto de Bosques de las Lomas y Arcos Bosques (El Pantalón) en medio de escuelas, universidades, hospitales, centros comerciales y toda la oferta de servicios que ofrecen Santa Fe y Bosques. Potencializa tu vida con nuestras amenidades: Alberca. Co-Working. Bar. Cafetería. Salón de Fiestas. Game Room. Chill Spot. Pet Zone. Área de asadores con fogateros. Gimnasio. Yoga Room. Motor Lobby. Sala de recepción. Concierge Vigilancia 24hrs. cctv. Shuttle que te conecta con los principales puntos de la cdmx y Santa Fe. Renta sin aval; Departamentos nuevos, Totalmente equipados con electrodomesticos nuevos, agenda una cita y prepara todo para estrenar!!",
  "status": "ONLINE",
  "listing_type": "DEVELOPMENT",
  "source_context": {
    "listing_url": "https://www.inmuebles24.com/propiedades/desarrollo/ememvein-ri-a-bosques-renta-y-estrena-nuestros-depas.-loft-1-141933064.html",
    "canonical_url": "https://www.inmuebles24.com/propiedades/desarrollo/ememvein-ri-a-bosques-renta-y-estrena-nuestros-depas.-loft-1-141933064.html",
    "domain": "inmuebles24.com",
    "seed_id": "6737f079bde6",
    "seed_type": "location",
    "seed_value": "ciudad de mexico",
    "page_index": 1,
    "scraped_time": "2026-04-27T22:04:54.149661+00:00"
  },
  "pricing": {
    "operations": [
      {
        "operation_type": {
          "id": 2,
          "name": "Renta"
        },
        "prices": [
          {
            "amount": 23500,
            "currency": "MN",
            "currency_id": 10
          }
        ]
      }
    ],
    "promotion_title": "1 Meses Gratis de Renta"
  },
  "property": {
    "type": {
      "id": 34,
      "name": "Desarrollos verticales"
    },
    "publication_area_id": 200,
    "reserved": false,
    "premier": false,
    "alternative_listing": false
  },
  "location": {
    "address": {
      "name": "Cuajimalpa de Morelos",
      "visibility": "EXACT"
    },
    "hierarchy": [
      {
        "id": "V1-D-23771",
        "name": "Santa Fe Cuajimalpa",
        "type": "ZONA",
        "depth": 3
      },
      {
        "id": "V1-C-516",
        "name": "Cuajimalpa de Morelos",
        "type": "CIUDAD",
        "depth": 2
      },
      {
        "id": "V1-B-69",
        "name": "Ciudad de México",
        "type": "PROVINCIA",
        "depth": 1,
        "acronym": "CDMX"
      },
      {
        "id": "V1-A-18",
        "name": "Mexico",
        "type": "PAIS",
        "depth": 0
      }
    ],
    "coordinates": {
      "latitude": 19.3376089,
      "longitude": -99.31138159999999
    }
  },
  "publisher": {
    "id": 102423242,
    "name": "Riğa Bosques",
    "url": "https://www.inmuebles24.com/inmobiliarias/ri-a-bosques_102423242-inmuebles.html",
    "type_id": 3,
    "logo_url": "https://img10.naventcdn.com/empresas/18/01/02/42/32/42/130x70/logo_riga_1700593764896.jpg",
    "premier": false,
    "approved": false,
    "created_at": "2023-09-28T04:00:00+00:00",
    "portal_id": 101
  },
  "publication": {
    "begin_at": "2025-01-21T18:21:01+00:00",
    "first_online_at": "2023-11-20T05:00:00+00:00",
    "modified_at": "2026-03-13T21:51:29-04:00",
    "plan_area_id": 200
  },
  "features": {
    "development": [
      {
        "category": "Desarrollo",
        "features": [
          {
            "id": "CFT201",
            "label": "Inmediata",
            "value": 0,
            "category_id": "CFC3"
          },
          {
            "id": "CFT202",
            "label": "Total de unidades",
            "value": 455,
            "category_id": "CFC3"
          },
          {
            "id": "CFT200",
            "label": "Listo para habitar",
            "value": 3,
            "category_id": "CFC3"
          }
        ]
      }
    ],
    "highlighted": [
      "Gimnasio",
      "Jardín",
      "Alberca",
      "Circuito Cerrado",
      "Estacionamientos",
      "Roof Garden"
    ],
    "flags": [
      {
        "id": "CFT200",
        "label": "Listo para habitar",
        "value": 3,
        "category_id": "CFC3"
      },
      {
        "id": "CFT201",
        "label": "Inmediata",
        "value": 0,
        "category_id": "CFC3"
      }
    ]
  },
  "media": {
    "primary_image_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574192.jpg?isFirstImage=true",
    "listing_logo_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/130x70/1140582052.jpg",
    "pictures": [
      {
        "type_id": 2,
        "order": 1,
        "width": 1536,
        "height": 1154,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574192.jpg?isFirstImage=true",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574192.jpg?isFirstImage=true",
        "title": "Desarrollo vertical , Cuajimalpa de Morelos · Riğa Bosques Renta y Estrena Nuestros Depas. (Loft, 1 y 2 Recámaras)"
      },
      {
        "type_id": 2,
        "order": 2,
        "width": 1600,
        "height": 1066,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574173.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574173.jpg",
        "title": "Desarrollo vertical en Santa Fe Cuajimalpa"
      },
      {
        "type_id": 2,
        "order": 3,
        "width": 1600,
        "height": 1072,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574170.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574170.jpg",
        "title": "Renta sin Aval en 24 horas. Proceso ágil y flexible. / Lease without guarantor w"
      },
      {
        "type_id": 2,
        "order": 4,
        "width": 764,
        "height": 1164,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574164.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574164.jpg",
        "title": "Desarrollo vertical"
      },
      {
        "type_id": 2,
        "order": 5,
        "width": 762,
        "height": 1150,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574165.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574165.jpg",
        "title": "Desarrollo vertical Santa Fe Cuajimalpa"
      },
      {
        "type_id": 2,
        "order": 6,
        "width": 1600,
        "height": 1066,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574178.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574178.jpg",
        "title": "Desarrollo vertical Santa Fe Cuajimalpa"
      },
      {
        "type_id": 2,
        "order": 7,
        "width": 1600,
        "height": 1070,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574175.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574175.jpg",
        "title": "Desarrollo vertical"
      },
      {
        "type_id": 2,
        "order": 8,
        "width": 760,
        "height": 1140,
        "large_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/720x532/1140574167.jpg",
        "medium_url": "https://img10.naventcdn.com/avisos/18/01/41/93/30/64/360x266/1140574167.jpg",
        "title": "Desarrollo vertical - Riğa Bosques"
      }
    ],
    "additional_picture_count": 29,
    "has_videos": false,
    "has_360_tour": true,
    "has_floor_plans": true
  },
  "contact": {
    "whatsapp": "52 5665850597",
    "show_anonymous_phone_lead": false,
    "whatsapp_posting_lead_enabled": true,
    "whatsapp_development_lead_enabled": true,
    "request_visit": {
      "modal_enabled": false,
      "postlead_modal_enabled": false
    }
  },
  "signals": {
    "publisher_slot": "aviso_sinslot_141933064",
    "pixel_plus": false,
    "early_demand_cronut": false
  },
  "attributes": {
    "alphanumeric_key": "5p6nc4"
  },
  "fingerprint": "0a5bbcdb38741b1559a2"
}
```

## Field Reference

### `listing`

- **type** *(string, required)*: record type.
- **id** *(number, required)*: listing identifier.
- **url** *(string, required)*: canonical public listing URL.
- **posting_code** *(string, optional)*: listing transaction label, such as rent or sale.
- **title** *(string, optional)*: public listing title.
- **generated_title** *(string, optional)*: normalized or category-derived title where available.
- **description** *(string, optional)*: public listing description.
- **status** *(string, optional)*: listing availability status.
- **listing_type** *(string, optional)*: listing category or placement type.
- **source_context.listing_url** *(string, optional)*: public listing URL captured for the record.
- **source_context.canonical_url** *(string, optional)*: canonical public URL for the listing.
- **source_context.domain** *(string, optional)*: source domain.
- **source_context.seed_id** *(string, optional)*: collection seed identifier.
- **source_context.seed_type** *(string, optional)*: input scope type used for collection.
- **source_context.seed_value** *(string, optional)*: input scope value used for collection.
- **source_context.page_index** *(number, optional)*: result page index associated with the record.
- **source_context.scraped_time** *(string, optional)*: ISO timestamp when the record was collected.
- **pricing.operations** *(array, optional)*: pricing groups by transaction operation.
- **pricing.operations.operation_type.id** *(number, optional)*: operation identifier.
- **pricing.operations.operation_type.name** *(string, optional)*: operation name.
- **pricing.operations.prices.amount** *(number, optional)*: listed price amount.
- **pricing.operations.prices.currency** *(string, optional)*: displayed currency label.
- **pricing.operations.prices.currency_id** *(number, optional)*: source currency identifier.
- **pricing.promotion_title** *(string, optional)*: public promotional price or incentive text.
- **property.type.id** *(number, optional)*: property type identifier.
- **property.type.name** *(string, optional)*: property type name.
- **property.publication_area_id** *(number, optional)*: publication area identifier.
- **property.reserved** *(boolean, optional)*: whether the listing is marked as reserved.
- **property.premier** *(boolean, optional)*: whether the listing is marked as premier.
- **property.alternative_listing** *(boolean, optional)*: whether the record is marked as an alternative listing.
- **location.address.name** *(string, optional)*: displayed address or location name.
- **location.address.visibility** *(string, optional)*: address visibility level.
- **location.hierarchy** *(array, optional)*: ordered geographic hierarchy for the listing.
- **location.hierarchy.id** *(string, optional)*: geographic unit identifier.
- **location.hierarchy.name** *(string, optional)*: geographic unit name.
- **location.hierarchy.type** *(string, optional)*: geographic unit type.
- **location.hierarchy.depth** *(number, optional)*: hierarchy depth.
- **location.hierarchy.acronym** *(string, optional)*: region acronym where available.
- **location.coordinates.latitude / location.coordinates.longitude** *(number, optional)*: geographic coordinates.
- **publisher.id** *(number, optional)*: publisher identifier.
- **publisher.name** *(string, optional)*: publisher name.
- **publisher.url** *(string, optional)*: public publisher URL.
- **publisher.type_id** *(number, optional)*: publisher type identifier.
- **publisher.logo_url** *(string, optional)*: publisher logo URL.
- **publisher.premier** *(boolean, optional)*: whether the publisher is marked as premier.
- **publisher.approved** *(boolean, optional)*: whether the publisher is marked as approved.
- **publisher.created_at** *(string, optional)*: publisher creation timestamp when available.
- **publisher.portal_id** *(number, optional)*: source portal identifier.
- **publication.begin_at** *(string, optional)*: listing publication start timestamp.
- **publication.first_online_at** *(string, optional)*: first online timestamp.
- **publication.modified_at** *(string, optional)*: last modified timestamp.
- **publication.plan_area_id** *(number, optional)*: publication plan area identifier.
- **features.development** *(array, optional)*: development-specific feature groups.
- **features.development.category** *(string, optional)*: feature group category.
- **features.development.features.id** *(string, optional)*: feature identifier.
- **features.development.features.label** *(string, optional)*: feature label.
- **features.development.features.value** *(number, optional)*: feature value.
- **features.development.features.category_id** *(string, optional)*: feature category identifier.
- **features.highlighted** *(array of strings, optional)*: highlighted amenities or attributes.
- **features.flags** *(array, optional)*: structured feature flags.
- **features.flags.id** *(string, optional)*: flag identifier.
- **features.flags.label** *(string, optional)*: flag label.
- **features.flags.value** *(number, optional)*: flag value.
- **features.flags.category_id** *(string, optional)*: flag category identifier.
- **media.primary_image_url** *(string, optional)*: primary listing image URL.
- **media.listing_logo_url** *(string, optional)*: listing logo or secondary image URL.
- **media.pictures** *(array, optional)*: listing image records.
- **media.pictures.type_id** *(number, optional)*: image type identifier.
- **media.pictures.order** *(number, optional)*: image order.
- **media.pictures.width / media.pictures.height** *(number, optional)*: image dimensions in pixels.
- **media.pictures.large_url / media.pictures.medium_url** *(string, optional)*: image URLs by size.
- **media.pictures.title** *(string, optional)*: image title or caption.
- **media.additional_picture_count** *(number, optional)*: count of additional pictures not included in the sample array.
- **media.has_videos** *(boolean, optional)*: whether videos are indicated for the listing.
- **media.has_360_tour** *(boolean, optional)*: whether a 360 tour is indicated for the listing.
- **media.has_floor_plans** *(boolean, optional)*: whether floor plans are indicated for the listing.
- **contact.whatsapp** *(string, optional)*: public WhatsApp contact value when available.
- **contact.show_anonymous_phone_lead** *(boolean, optional)*: whether anonymous phone lead behavior is indicated.
- **contact.whatsapp_posting_lead_enabled** *(boolean, optional)*: whether WhatsApp posting leads are enabled.
- **contact.whatsapp_development_lead_enabled** *(boolean, optional)*: whether WhatsApp development leads are enabled.
- **contact.request_visit.modal_enabled** *(boolean, optional)*: whether request-visit modal behavior is indicated.
- **contact.request_visit.postlead_modal_enabled** *(boolean, optional)*: whether post-lead visit modal behavior is indicated.
- **signals.publisher_slot** *(string, optional)*: publisher slot signal.
- **signals.pixel_plus** *(boolean, optional)*: source-provided listing signal.
- **signals.early_demand_cronut** *(boolean, optional)*: source-provided listing signal.
- **attributes.alphanumeric_key** *(string, optional)*: source-provided alphanumeric listing key.
- **fingerprint** *(string, optional)*: stable record fingerprint for change tracking.

## Data Quality, Guarantees, And Handling

- **Structured records:** results are normalized into predictable JSON objects for downstream use.
- **Best-effort extraction:** fields may vary by region, session, availability, and public UI experiments.
- **Optional fields:** null-check optional fields in downstream code because sparse listings may not provide every attribute.
- **Deduplication:** use `type + ":" + id` as the recommended idempotency key.
- **Freshness:** results reflect the publicly available data at run time.
- **Repeated runs:** use the recommended idempotency key when syncing data into warehouses, CRMs, or search indexes.

## Tips For Best Results

- Start with a small `limit` to validate the output shape before scaling up.
- Use one geography, property segment, or deal type per run when you need cleaner segmentation.
- Leave optional filters empty when the goal is broad discovery.
- Add filters gradually to understand how each field changes coverage.
- Use `publication_date` and `sort_by` for monitoring recently posted or recently updated inventory.
- Schedule recurring runs for monitoring workflows instead of relying on manual one-off jobs.
- Use `type + ":" + id` for deduplication when storing results over time.

## How to Run on Apify

1. Open the Actor in Apify Console.
2. Configure the available input fields for the target scope.
3. Set the maximum number of outputs to collect with `limit`.
4. Click **Start** and wait for the run to finish.
5. Download results in JSON, CSV, Excel, or other supported formats.

## Scheduling & Automation

### Scheduling

**Automated Data Collection**

Schedule runs to keep real estate listing datasets fresh for monitoring, reporting, enrichment, and recurring analysis. Use a consistent input configuration when you need comparable results across time periods.

- Navigate to **Schedules** in Apify Console
- Create a new schedule, such as daily, weekly, or custom cron
- Configure input parameters
- Enable notifications for run completion
- Add webhooks for automated processing

### Integration Options

- **CRM enrichment:** sync public listing, publisher, location, and contact attributes into account or lead records.
- **BI dashboards:** monitor pricing, availability, publication recency, property types, and geographic coverage over time.
- **Data warehouses:** store repeated runs for historical analysis, deduplication, and long-term trend modeling.
- **Google Sheets or Airtable:** review smaller listing batches, qualify leads, or share curated market snapshots with operations teams.
- **Webhooks:** trigger ingestion, validation, notification, or alerting workflows after each completed run.
- **Data enrichment pipelines:** append current public real estate attributes to existing CRM, analytics, or market intelligence datasets.

## Export Formats And Downstream Use

Apify datasets can be exported or consumed by downstream systems, making the actor suitable for both manual review and automated data delivery.

- **JSON:** for APIs, applications, and data pipelines.
- **CSV or Excel:** for spreadsheet workflows and manual review.
- **API access:** for automated ingestion into internal systems.
- **BI and warehouses:** for reporting, dashboards, and historical analysis.

## Performance

Estimated run times:

- **Small runs (< 1,000 outputs):** ~3–5 minutes
- **Medium runs (1,000–5,000 outputs):** ~5–15 minutes
- **Large runs (5,000+ outputs):** ~15–30 minutes

Execution time varies based on filters, result volume, and how much information is returned per record. Highly filtered runs can finish faster, while broad discovery or detail-rich records may take longer.

## Limitations

- Availability depends on what [https://www.inmuebles24.com](https://www.inmuebles24.com) publicly exposes at run time.
- Some optional fields may be missing on sparse records or specific listing types.
- Very broad searches may take longer or require higher limits to reach the desired coverage.
- Target-side changes can affect field availability, naming, or visible attributes.
- Regional, account, or availability differences may change visible results.
- Public listings can be modified, removed, reserved, or republished between runs.

## Troubleshooting

- **No results returned:** check filters, location spelling, property category choices, and whether Inmuebles24 has matching public records for the selected scope.
- **Fewer results than expected:** broaden filters, raise `limit`, or verify that the target contains enough matching records.
- **Some fields are empty:** optional fields depend on what each record publicly provides.
- **Run takes longer than expected:** reduce scope, lower `limit` for validation, or split broad collection into smaller segments.
- **Output changed:** compare the current output with the field reference and report a small sample if support is needed.

## FAQ

### What data does this actor collect?

It collects public Inmuebles24 real estate listing records, including listing identifiers, titles, descriptions, prices, locations, property details, publisher information, publication metadata, media indicators, contact-related public fields, and source URLs.

### Can I filter by location, category, date, price, or other criteria?

Yes. The actor supports location, deal type, sorting, seller type, multimedia requirements, view, building age, publication date, property type, bedroom count, bathroom count, parking, price range, building area, land area, and result limit.

### Why did I receive fewer results than my limit?

The selected scope may contain fewer public matching listings than the requested `limit`, or your filters may be narrow. Broaden the input or increase coverage gradually after validating the first results.

### Can I schedule recurring runs?

Yes. Use Apify schedules to run the actor daily, weekly, or on a custom cron schedule for monitoring, reporting, and repeated enrichment workflows.

### How do I avoid duplicates across runs?

Use `type + ":" + id` as the idempotency key when inserting or updating records in your destination system.

### Can I export the data to CSV, Excel, or JSON?

Yes. Apify datasets support exports in JSON, CSV, Excel, and other supported formats.

### Does this actor collect private data?

The actor is intended to collect publicly available listing information from Inmuebles24. Users are responsible for using the data lawfully and respecting privacy and applicable platform terms.

### What should I include when reporting an issue?

Include the input used with any sensitive values redacted, the run ID, expected versus actual behavior, and a small output sample if it helps illustrate the issue.

## Compliance & Ethics

### Responsible Data Collection

This actor collects publicly available **real estate listing** information from **[https://www.inmuebles24.com](https://www.inmuebles24.com)** for legitimate business purposes, including:

- **Real estate** research and market analysis
- Listing monitoring, pricing analysis, and inventory tracking
- CRM enrichment, lead qualification, and operational reporting

This section is informational and not legal advice.

### Best Practices

- Use collected data in accordance with applicable laws, regulations, and the target site's terms.
- Respect individual privacy and personal information.
- Use data responsibly and avoid disruptive or excessive collection.
- Do not use this actor for spamming, harassment, or other harmful purposes.
- Follow relevant data protection requirements where applicable, such as GDPR and CCPA.

## Support

For help, use the actor page or Issues. Include the input used with sensitive values redacted, the run ID, expected versus actual behavior, and a small output sample when available. Avoid sharing unnecessary personal data in support requests.