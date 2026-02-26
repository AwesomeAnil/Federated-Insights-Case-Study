# Enterprise Airline Analytics – Architecture Overview

This architecture demonstrates integration of commercial demand, operational execution, and financial performance into a governed semantic analytics layer.

```mermaid
flowchart LR

    subgraph Source Systems
        A1[Booking System]
        A2[Flight Operations System]
        A3[Financial System]
    end

    subgraph Data Layer
        B1[Fact_Bookings]
        B2[Fact_Flights]
        B3[Fact_Financials]
        D1[Dim_Date]
        D2[Dim_Route]
        D3[Dim_FareClass]
        D4[Dim_CustomerSegment]
        D5[Dim_Aircraft]
    end

    subgraph Semantic Layer
        S1[Conformed Dimensions]
        S2[Reusable KPI Measures]
        S3[Certified Metrics]
    end

    subgraph Analytics Layer
        R1[Executive Dashboard]
        R2[Route Performance Analysis]
        R3[Operational Monitoring]
        R4[Profitability & Margin Analysis]
    end

    A1 --> B1
    A2 --> B2
    A3 --> B3

    B1 --> S1
    B2 --> S1
    B3 --> S1

    S1 --> S2
    S2 --> S3

    S3 --> R1
    S3 --> R2
    S3 --> R3
    S3 --> R4