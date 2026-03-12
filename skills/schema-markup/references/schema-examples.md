# Schema Examples — Complete JSON-LD Reference

This file contains production-ready JSON-LD examples for each common page type. Load this file when you need complete code examples to provide to the user.

## Table of Contents

1. [Homepage — Organization + WebSite](#homepage)
2. [Blog Post — Article with Author](#blog-post)
3. [Product Page](#product-page)
4. [FAQ Page](#faq-page)
5. [SaaS / Software Page](#saas-page)
6. [Local Business](#local-business)
7. [How-To / Tutorial](#how-to)
8. [Category / Listing Page](#category-page)
9. [Full @graph Example — Multi-type Page](#full-graph)

---

## Homepage — Organization + WebSite {#homepage}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://example.com/#organization",
      "name": "Example Corp",
      "url": "https://example.com",
      "logo": {
        "@type": "ImageObject",
        "url": "https://example.com/logo.png",
        "width": 600,
        "height": 60
      },
      "description": "Brief description of what the company does",
      "foundingDate": "2020",
      "numberOfEmployees": {
        "@type": "QuantitativeValue",
        "value": 50
      },
      "areaServed": "Global",
      "knowsAbout": [
        "topic 1",
        "topic 2",
        "topic 3"
      ],
      "sameAs": [
        "https://www.linkedin.com/company/example",
        "https://twitter.com/example",
        "https://www.facebook.com/example",
        "https://www.youtube.com/@example",
        "https://en.wikipedia.org/wiki/Example_Corp",
        "https://www.wikidata.org/wiki/Q12345678",
        "https://www.crunchbase.com/organization/example"
      ],
      "contactPoint": {
        "@type": "ContactPoint",
        "telephone": "+1-800-555-0100",
        "contactType": "customer service",
        "availableLanguage": ["English"]
      }
    },
    {
      "@type": "WebSite",
      "@id": "https://example.com/#website",
      "name": "Example Corp",
      "url": "https://example.com",
      "publisher": { "@id": "https://example.com/#organization" },
      "potentialAction": {
        "@type": "SearchAction",
        "target": {
          "@type": "EntryPoint",
          "urlTemplate": "https://example.com/search?q={search_term_string}"
        },
        "query-input": "required name=search_term_string"
      }
    }
  ]
}
```

**Notes:**
- `SearchAction` enables the sitelinks search box in Google. Only add if your site has a working search feature at that URL pattern.
- `sameAs` — include every verifiable official external profile. Wikipedia/Wikidata are the strongest signals for Knowledge Panel generation.
- `knowsAbout` — list your core expertise areas. This helps AI systems understand your topical authority.
- `logo` should meet Google's requirements: min 112×112px for square logos, or use the full-width version.

---

## Blog Post — Article with Author {#blog-post}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Article",
      "@id": "https://example.com/blog/article-slug/#article",
      "headline": "Article Title — Keep Under 110 Characters",
      "description": "A concise summary of the article in 1-2 sentences.",
      "image": {
        "@type": "ImageObject",
        "url": "https://example.com/images/article-hero.jpg",
        "width": 1200,
        "height": 630
      },
      "datePublished": "2025-03-01T09:00:00+00:00",
      "dateModified": "2025-03-05T14:30:00+00:00",
      "author": {
        "@type": "Person",
        "@id": "https://example.com/about/jane-smith/#person",
        "name": "Jane Smith",
        "url": "https://example.com/about/jane-smith",
        "jobTitle": "Head of Research",
        "worksFor": { "@id": "https://example.com/#organization" },
        "sameAs": [
          "https://www.linkedin.com/in/janesmith",
          "https://twitter.com/janesmith"
        ]
      },
      "publisher": { "@id": "https://example.com/#organization" },
      "mainEntityOfPage": {
        "@type": "WebPage",
        "@id": "https://example.com/blog/article-slug/#webpage"
      },
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": [".article-summary", ".key-takeaway", "h1"]
      },
      "isPartOf": { "@id": "https://example.com/#website" }
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://example.com/blog/article-slug/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Blog",
          "item": "https://example.com/blog"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Article Title"
        }
      ]
    }
  ]
}
```

**Notes:**
- `author` must be a `Person` object (not a plain string). This is critical for E-E-A-T and AI attribution.
- `speakable` — point cssSelector at the most quotable parts of your article. Good candidates: the summary paragraph, definition sections, key findings. Bad candidates: navigation, footer, sidebar.
- The last BreadcrumbList item should NOT have an `item` URL (it represents the current page).
- `dateModified` — update this when content actually changes. Google uses it to determine freshness.

---

## Product Page {#product-page}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Product",
      "@id": "https://example.com/products/widget-pro/#product",
      "name": "Widget Pro",
      "description": "Brief product description",
      "image": [
        "https://example.com/images/widget-pro-1.jpg",
        "https://example.com/images/widget-pro-2.jpg"
      ],
      "sku": "WIDGET-PRO-001",
      "brand": {
        "@type": "Brand",
        "name": "Example Corp"
      },
      "offers": {
        "@type": "Offer",
        "url": "https://example.com/products/widget-pro",
        "priceCurrency": "USD",
        "price": "49.99",
        "availability": "https://schema.org/InStock",
        "priceValidUntil": "2026-12-31",
        "seller": { "@id": "https://example.com/#organization" }
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.7",
        "reviewCount": "142"
      },
      "review": [
        {
          "@type": "Review",
          "author": {
            "@type": "Person",
            "name": "Real Customer Name"
          },
          "datePublished": "2025-02-15",
          "reviewRating": {
            "@type": "Rating",
            "ratingValue": "5"
          },
          "reviewBody": "Actual review text from the page"
        }
      ]
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://example.com/products/widget-pro/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Products",
          "item": "https://example.com/products"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Widget Pro"
        }
      ]
    }
  ]
}
```

**Notes:**
- `aggregateRating` and `review` — ONLY include if real reviews are visible on the page. Fake or hidden reviews violate Google's policies.
- `availability` — always include. Use appropriate schema.org values: `InStock`, `OutOfStock`, `PreOrder`, `BackOrder`.
- Multiple images are encouraged — Google may use them in different display formats.
- `price` should be a string, not a number. Include `priceCurrency` always.

---

## FAQ Page {#faq-page}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "FAQPage",
      "@id": "https://example.com/faq/#faqpage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "What is your return policy?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "We offer a 30-day money-back guarantee on all purchases. Contact support@example.com to initiate a return."
          }
        },
        {
          "@type": "Question",
          "name": "How long does shipping take?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "Standard shipping takes 5-7 business days. Express shipping is available for 2-3 business day delivery."
          }
        },
        {
          "@type": "Question",
          "name": "Do you offer international shipping?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "Yes, we ship to over 50 countries. International shipping typically takes 10-14 business days."
          }
        }
      ]
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://example.com/faq/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "FAQ"
        }
      ]
    }
  ]
}
```

**Notes:**
- Keep answers concise and direct. Google truncates long answers in FAQ rich results. AI systems prefer clear, quotable answers.
- Every Q&A pair in the schema must have a matching visible question and answer on the page.
- You can add FAQPage schema to product pages, service pages — anywhere a FAQ section exists. It doesn't have to be a dedicated FAQ page.
- For AEO: FAQ schema is one of the best ways to get your answers surfaced by AI systems, because Q&A pairs map directly to how users query LLMs.

---

## SaaS / Software Page {#saas-page}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "SoftwareApplication",
      "@id": "https://example.com/product/#software",
      "name": "Example App",
      "description": "Brief description of what the software does",
      "applicationCategory": "BusinessApplication",
      "operatingSystem": "Web, iOS, Android",
      "url": "https://example.com/product",
      "offers": {
        "@type": "AggregateOffer",
        "lowPrice": "0",
        "highPrice": "99",
        "priceCurrency": "USD",
        "offerCount": "3"
      },
      "aggregateRating": {
        "@type": "AggregateRating",
        "ratingValue": "4.8",
        "ratingCount": "1250",
        "bestRating": "5"
      },
      "creator": { "@id": "https://example.com/#organization" }
    }
  ]
}
```

**Notes:**
- `applicationCategory` — use Google's supported values: `BusinessApplication`, `GameApplication`, `DesignApplication`, `DeveloperApplication`, `EducationalApplication`, etc.
- `AggregateOffer` is useful when you have multiple pricing tiers (free, pro, enterprise).
- `aggregateRating` — only include if you have real ratings (e.g., from app stores, review platforms like G2/Capterra) and they're displayed on the page.

---

## Local Business {#local-business}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "LocalBusiness",
      "@id": "https://example.com/#localbusiness",
      "name": "Example Bakery",
      "description": "Artisan bakery specializing in sourdough bread and pastries",
      "url": "https://example.com",
      "telephone": "+1-555-123-4567",
      "address": {
        "@type": "PostalAddress",
        "streetAddress": "123 Main Street",
        "addressLocality": "Portland",
        "addressRegion": "OR",
        "postalCode": "97201",
        "addressCountry": "US"
      },
      "geo": {
        "@type": "GeoCoordinates",
        "latitude": 45.5231,
        "longitude": -122.6765
      },
      "openingHoursSpecification": [
        {
          "@type": "OpeningHoursSpecification",
          "dayOfWeek": ["Monday", "Tuesday", "Wednesday", "Thursday", "Friday"],
          "opens": "07:00",
          "closes": "18:00"
        },
        {
          "@type": "OpeningHoursSpecification",
          "dayOfWeek": ["Saturday", "Sunday"],
          "opens": "08:00",
          "closes": "16:00"
        }
      ],
      "priceRange": "$$",
      "image": "https://example.com/images/storefront.jpg",
      "sameAs": [
        "https://www.google.com/maps/place/?q=place_id:ChIJ...",
        "https://www.yelp.com/biz/example-bakery",
        "https://www.instagram.com/examplebakery"
      ]
    }
  ]
}
```

**Notes:**
- Use the most specific `@type` available: `Restaurant`, `Bakery`, `DentalClinic`, `LegalService`, etc. These are subtypes of `LocalBusiness`.
- `geo` coordinates help Google match your business to map results.
- `sameAs` for local businesses should include Google Maps/Places link, Yelp, TripAdvisor, and social profiles.
- `priceRange` uses $ symbols ($, $$, $$$, $$$$).

---

## How-To / Tutorial {#how-to}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "HowTo",
      "@id": "https://example.com/how-to/make-sourdough/#howto",
      "name": "How to Make Sourdough Bread",
      "description": "Step-by-step guide to baking sourdough bread from scratch",
      "totalTime": "PT24H",
      "estimatedCost": {
        "@type": "MonetaryAmount",
        "currency": "USD",
        "value": "5"
      },
      "image": "https://example.com/images/sourdough-final.jpg",
      "step": [
        {
          "@type": "HowToStep",
          "name": "Make the starter",
          "text": "Mix equal parts flour and water. Let it ferment at room temperature for 24 hours.",
          "image": "https://example.com/images/step-1.jpg"
        },
        {
          "@type": "HowToStep",
          "name": "Mix the dough",
          "text": "Combine starter with flour, water, and salt. Mix until a shaggy dough forms.",
          "image": "https://example.com/images/step-2.jpg"
        },
        {
          "@type": "HowToStep",
          "name": "Bulk fermentation",
          "text": "Let the dough rise for 4-6 hours at room temperature, performing stretch and folds every 30 minutes for the first 2 hours."
        }
      ]
    }
  ]
}
```

**Notes:**
- `totalTime` uses ISO 8601 duration format: `PT30M` (30 minutes), `PT2H` (2 hours), `PT1H30M` (1.5 hours).
- Each step should have `name` (short title) and `text` (detailed instruction). Images per step are recommended but not required.
- HowTo rich results are competitive — Google often shows them as visual carousels.

---

## Category / Listing Page {#category-page}

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "CollectionPage",
      "@id": "https://example.com/products/category/#collectionpage",
      "name": "Category Name",
      "description": "Browse our collection of...",
      "isPartOf": { "@id": "https://example.com/#website" }
    },
    {
      "@type": "ItemList",
      "@id": "https://example.com/products/category/#itemlist",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Product One",
          "url": "https://example.com/products/product-one"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Product Two",
          "url": "https://example.com/products/product-two"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Product Three",
          "url": "https://example.com/products/product-three"
        }
      ]
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://example.com/products/category/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Products",
          "item": "https://example.com/products"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Category Name"
        }
      ]
    }
  ]
}
```

---

## Full @graph Example — Article Page with All Connections {#full-graph}

This example shows how a complete article page schema looks when all entities are properly connected:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Organization",
      "@id": "https://example.com/#organization",
      "name": "Example Corp",
      "url": "https://example.com",
      "logo": {
        "@type": "ImageObject",
        "url": "https://example.com/logo.png"
      },
      "knowsAbout": ["topic 1", "topic 2"],
      "sameAs": [
        "https://linkedin.com/company/example",
        "https://twitter.com/example"
      ]
    },
    {
      "@type": "WebSite",
      "@id": "https://example.com/#website",
      "name": "Example Corp",
      "url": "https://example.com",
      "publisher": { "@id": "https://example.com/#organization" }
    },
    {
      "@type": "WebPage",
      "@id": "https://example.com/blog/guide/#webpage",
      "url": "https://example.com/blog/guide",
      "name": "Page Title",
      "isPartOf": { "@id": "https://example.com/#website" },
      "breadcrumb": { "@id": "https://example.com/blog/guide/#breadcrumb" }
    },
    {
      "@type": "Article",
      "@id": "https://example.com/blog/guide/#article",
      "headline": "Complete Guide to...",
      "description": "Summary of the article",
      "image": "https://example.com/images/hero.jpg",
      "datePublished": "2025-06-01T09:00:00+00:00",
      "dateModified": "2025-06-10T15:00:00+00:00",
      "author": {
        "@type": "Person",
        "@id": "https://example.com/team/jane/#person",
        "name": "Jane Smith",
        "jobTitle": "Head of Content",
        "worksFor": { "@id": "https://example.com/#organization" },
        "knowsAbout": ["content strategy", "SEO"],
        "sameAs": ["https://linkedin.com/in/janesmith"]
      },
      "publisher": { "@id": "https://example.com/#organization" },
      "mainEntityOfPage": { "@id": "https://example.com/blog/guide/#webpage" },
      "speakable": {
        "@type": "SpeakableSpecification",
        "cssSelector": [".article-summary", ".key-takeaway"]
      }
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://example.com/blog/guide/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://example.com"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Blog",
          "item": "https://example.com/blog"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Complete Guide to..."
        }
      ]
    }
  ]
}
```

This is the gold standard: every entity has an `@id`, every relationship uses `@id` references, Organization and Person have `knowsAbout` for AI topical authority, Article has `speakable` for AEO, and the breadcrumb trail provides structural context.
