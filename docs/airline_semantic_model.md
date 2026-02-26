# Enterprise Airline Analytics – Semantic Model

This model integrates daily commercial demand, operational performance, and monthly financials into a conformed dimensional architecture supporting executive airline analytics.

```mermaid
erDiagram

    Dim_Date ||--o{ Fact_Bookings : filters
    Dim_Date ||--o{ Fact_Flights : filters
    Dim_Date ||--o{ Fact_Financials : filters_monthly

    Dim_Route ||--o{ Fact_Bookings : route
    Dim_Route ||--o{ Fact_Flights : route
    Dim_Route ||--o{ Fact_Financials : route

    Dim_FareClass ||--o{ Fact_Bookings : fare
    Dim_CustomerSegment ||--o{ Fact_Bookings : segment

    Dim_Aircraft ||--o{ Fact_Flights : aircraft

    Dim_Route ||--o{ Dim_Airport : origin_destination


    Dim_Date {
        date Date PK
        string YearMonth
        string Season_Label
        int Year_Index
    }

    Dim_Route {
        string Route_ID PK
        string Origin
        string Destination
        int Distance_km
    }

    Dim_FareClass {
        int Fare_Class_ID PK
        string Fare_Class
        string Cabin_Group
    }

    Dim_CustomerSegment {
        int Segment_ID PK
        string Segment_Name
    }

    Dim_Aircraft {
        string Aircraft_Type PK
        int Seats_Total
    }

    Dim_Airport {
        string Airport_Code PK
        string City
        string Country
    }

    Fact_Bookings {
        date Booking_Date FK
        string Route_ID FK
        int Fare_Class_ID FK
        int Segment_ID FK
        int Tickets_Sold
        float Total_Revenue
    }

    Fact_Flights {
        date Flight_Date FK
        string Route_ID FK
        string Aircraft_Type FK
        int Seats_Sold
        int Seats_Capacity
        int Departure_Delay_Minutes
    }

    Fact_Financials {
        string YearMonth FK
        string Route_ID FK
        float Fuel_Cost
        float Staff_Cost
        float Airport_Fees
        float Total_Cost
    }