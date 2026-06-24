Loyalty Promotions

Copy Page
Loyalty Promotions are time-bound programs designed to reward members with incentives, such as bonus points or coupons beyond standard program benefits. These promotions drive engagement and sales by triggering rewards for specific activities, including transactions, reaching milestones, or updating profiles.

What you can do
You can use the Loyalty Promotions APIs to:

Create and Update: You can create and update unified promotions with various earning rules, including single or grouped activities, to meet your specific requirements.
Manage Enrollment: You can configure the promotion with opt-in enrollment, allowing members to join via transactions, audience lists, or direct API calls.
Review and Approve: Review and approve promotions to transition them from draft to active states using the review workflow.
Search and Filter: Search for promotions using text-based queries and status filters for efficient management.
Configure Limits: You can configure limits for enrollments, points, and redemptions at the user, promotion, or activity level.
Split Liability: You can split liability for rewards between different programs or partners to balance costs.
Note: Deletion is not supported through these APIs. Promotions should be managed through status updates; for example, you can set the status as EXPIRED

Search behaviour
Search across Loyalty Promotions APIs uses text-based matching and status filtering.

When you pass a search query:

searchText: The API filters promotions by name or description containing the specific keywords (e.g., "Holiday Bonus").
status: You can filter by specific states such as DRAFT, ACTIVE, PAUSED, PENDING_APPROVAL, LIVE, or UPCOMING.
includeDraftDetails: Set this to true to retrieve the unpublished draft information of a live promotion.
Promotion Structure
The Loyalty Promotions APIs utilize three major structures to define the logic of how rewards are earned:

Activities
These are the specific actions a customer must perform to trigger a reward. These can be configured in two ways:

Single Activity: A standalone requirement.

Example: Spend $100 in a single transaction to receive a 12% discount.

Group Activity: Multiple requirements that must be met together.

Example: Spend $100 and purchase two items from the "Footwear" category to receive a 12% discount.

Cycles
Cycles define the specific validity period for individual activities or the promotion as a whole.

Example: A 14-day window during a "New Year" campaign where all required activities must be completed to qualify for rewards.

Milestones
Milestones are used to track a user's incremental progress toward a reward within a defined cycle.
Example: Hitting a $500 spend mark to automatically trigger a tier upgrade from "Silver" to "Gold" status.

Enrolment Models
The APIs support different enrolment methods to determine how members are enrolled into a promotion:

TRANSACTION: Automatically enrols members when they perform a qualifying purchase.
OPT_IN: Members are enrolled via an API call or external trigger.
AUDIENCE: Audience enrollment automatically signs up members for a promotion based on their audience group, requiring no manual action from the user.
Example: Pre-enrolling all "Gold Tier" members for a festive sale.

Limits and Liability
You can set limits and split the liability of a particular promotion for budget control and fraud prevention:

1. Limits
Defines the limits for rewards to control the budget and prevent over-redemption by restricting the count or frequency.

Limits are applied at three distinct levels:
User Level:
Restricts how much a single customer can earn.
Example: A member can earn a maximum of 500 points per month (Frequency) or is limited to 3 "Refer-a-Friend" bonuses total (Count).

Promotion Level:
Restricts the total promotion amount for the entire campaign budget.
Example: The first 10,000 customers to shop get a free voucher; once hit, the promotion will end.

Earn Level:
Restricts a specific earning rule within a promotion.
Example: In a "Double Points" weekend, the "Double" bonus is limited to the first $200 spent per transaction.

2. Liability Split
Distributes the financial cost of a reward across different business units or external partners using the liabilityOwnerSplitInfo object.

Example: For a "Co-branded Credit Card" promotion, the Bank pays 70% of the points cost, and the Retailer pays 30%.

Pagination
All list and search APIs enforce pagination.

Default size is 10.
Use page (0-indexed) to retrieve the next set of records.
Batch support is not available for retrieval.
QuickStart: set up promotions using the Loyalty Promotions APIs
Use this sequence to configure and launch a new loyalty campaign.

Step 1: Create a promotion
Use the Create a Loyalty Promotion to define the promotion's metadata, earning rules (activities), and validity period. The promotion will be created in DRAFT status.

Step 2: Refine configuration
Use the Update a Loyalty Promotion to update limits, add liability splits, or modify enrolment criteria before the promotion goes live.

Step 3: Review and Approve
Use the Review API to submit an APPROVE action. This transitions the promotion from DRAFT or PENDING_APPROVAL to ACTIVE.

Step 4: Enrol Members
If the promotion requires manual entry, use the Enrol API to add members or trigger an opt-in.

Step 5: Retrieve and Verify
Use the GET APIs to search for the promotion by ID or text (searchText) to verify its status and configuration details.

Create a Loyalty Promotion
POST
Review a Loyalty Promotion
POST
Enrol Members
POST
Update Promotion
PUT
Get Details (ID)
GET
List Member Promotions
GET
Get Member Promotion Explode Details
GET

Old Loyalty Promotions
The Loyalty Promotion are of three types:

Available without issue - Accessible to all customers and automatically triggered based on predefined rules, behavioural events, or milestone completions. Benefits such as points, tier upgrades, coupons, or badges are directly provided when customers meet the defined criteria.
Direct issue - A specific promotion is issued to customers based on their behaviour or transactions. Customers must meet the criteria during a future transaction to receive the benefits. This process is initiated through workflows like TransactionAdd or Behavioral events.
Enroll & Issue - Requires customers to opt in or enrol before receiving a promotion. Involves three steps: enrollment, completing specific actions, and receiving benefits. These promotions engage customers through an interactive approach, targeting specific audiences.
Type of Promotion	API for Single Issuance and Enrolment	API for Bulk Issuance and Enrolment (Can be also used for Single Issual and Enrolment)	API for Revoking Promotion
Available without issue	-	-	-
Direct issue	v2/promotion/issue - Promotion type should be LOYALTY	v2/promotion/bulk/directEarn- Promotion type should be LOYALTY	v2/promotion/bulk/revokeDirectEarn
Enroll & Issue	v2/promotion/issue - Promotion type should be LOYALTY_EARNING	v2/promotion/bulk/enrolAndEarn- Promotion type should be LOYALTY_EARNING	v2/promotion/bulk/revokeEnrolAndEarn
Terminologies
The table below highlights backend terminologies and their corresponding terms used in the UI/frontend:

UI/Frontend terminology	Backend terminology	Description
Enrol	Issue	The customer is enrolled into a promotion.
Issue	Earn	The customer completes the required activity to earn the promotion. Once the promotion is earned, the customer can fulfil the criteria to receive the associated benefits.
Note: For Direct issue promotions, reward points are only credited after the promotion has been issued to the customer. Triggering the tracker event alone does not award points.

For more information and use cases, refer to the user documentation on Loyalty Promotions.