# Reserved Instance billing {#concept_t2m_n4q_dgb .concept}

Reserved Instances support multiple payment options and are billed according to their applicable hourly rates. This topic describes the billing details of Reserved Instances.

## Payment options and billing {#section_hjx_m5q_dgb .section}

The following table shows the payment options and hourly charges of Reserved Instances:

|Item|All Upfront|Partial Upfront|No Upfront|
|----|-----------|---------------|----------|
|Applicable qualifications|N/A|N/A|Your Alibaba Cloud account needs to reach a certain level.|
|Payment method|Full payment is made upon purchase, with no other costs or additional hourly charges incurred for the entire term.|A portion of the cost must be paid upon purchase. You are also billed the Reserved Instance hourly rate for every hour within the term.|You are billed the Reserved Instance hourly rate for every hour within the term. No upfront payment is required.|
|Upfront payment|Deducted upon purchase. The specific amount is subject to the specifications you selected on the purchase page.|Deducted upon purchase. The specific amount is subject to the specifications you selected on the purchase page.|N/A|
|Reserved Instance hourly charges|N/A|Charged on a second basis, billed on an hourly basis, and paid on a monthly basis. The specific hourly rate is subject to the specifications you selected on the purchase page.If your fees incurred have reached USD 1,000, USD 1,000 will be automatically deducted from your account. Any amount that is less than USD 1,000 is included in the monthly bill.

|Charged on a second basis, billed on an hourly basis, and paid on a monthly basis. The specific hourly rate is subject to the specifications you selected on the purchase page.If your fees incurred have reached USD 1,000, USD 1,000 will be automatically deducted from your account. Any amount that is less than USD 1,000 is included in the monthly bill.

|
|Currency|USD|USD|USD|

## Billing rules {#section_zgp_ncw_fgb .section}

Once the Reserved Instance is purchased successfully, calculation of the reservation term begins. You are charged according to your payment option regardless of whether Pay-As-You-Go instances are matched. Choosing All Upfront reduces costs.

An RI takes effect and is billed on the hour upon successful purchase. It expires at 00:00:00 the day after the term end date. For example, you purchased an RI on February 26, 2019 13:45:00 PM, with a term of one year. The RI took effect on 2019-02-26 13:00:00, and its billing also started from that time. It will expire on 2020-02-27 00:00:00. If you had matchable instances when you purchased the RI, the billing discount first applied to the bill generated from 13:00 to 14:00 on February 26, 2019 till the expiration of the RI.

## Claim a refund {#section_rqb_bwq_dgb .section}

You can claim a refund in the following case:

-   The instance resources are in short supply in the target region or zone after you have purchased, split, or merged Reserved Instances, or adjusted the Reserved Instance scope.

The fees incurred will be deducted from the claimed refund. In addition, a refund fee \(15% of the refundable amount\) is charged. If you chose Partial Upfront as the payment method, and you have outstanding fees due to the Reserved Instance hourly rate, you need to pay off those fees before receiving the refund.

**Note:** If you purchased Reserved Instances in your local currency, the refundable amount is converted at the latest exchange rate before being returned to you in your local currency.

