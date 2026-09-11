# How to Design Better APIs

Designing a good API is not only about defining endpoints and choosing HTTP methods.

An API is a contract between a service and the people or systems that consume it. If that contract is unclear, inconsistent or difficult to understand, developers have to spend more time working out how the API behaves, and documentation becomes harder to write and maintain.

Good API design starts with understanding what the API needs to achieve and who will use it.

This article outlines some practical principles that can make APIs easier to use, document and maintain.

## 1. Start with the use case

Before defining an endpoint, understand what the consumer needs to accomplish.

Ask:

- What does the user or system need to do?
- What information is required?
- What information will the API return?
- What should happen when something goes wrong?
- Are there constraints or dependencies that need to be defined?

For example, instead of starting with a database structure, start with the task:

> A client needs to retrieve information about a customer using the customer's ID.

This gives you a clearer basis for defining the API.

The API should support the user's task rather than simply expose the underlying implementation.

## 2. Define requirements before designing the API

API design should be based on clear requirements.

Requirements should establish what the API must do and what constraints apply.

For example:

**Functional requirement**

The API must allow a client to retrieve a customer by ID.

**Input requirement**

The client must provide a valid customer ID.

**Output requirement**

The API must return the customer's available account information.

**Error requirement**

The API must return an appropriate response when the customer cannot be found.

Defining these requirements first makes it easier to evaluate whether the resulting API actually meets the intended need.

It also provides useful input for both development and documentation.

## 3. Use clear and consistent resource names

Resource names should be predictable.

For example:

    /customers
    /customers/{customerId}
    /customers/{customerId}/orders

Once a developer understands the naming convention, they should be able to make reasonable assumptions about related resources.

Avoid unnecessary variations such as:

    /getCustomer
    /customerDetails
    /retrieve-customer

if the rest of the API uses resource-oriented naming.

Consistency reduces the amount of information developers need to learn.

## 4. Use HTTP methods consistently

HTTP methods should clearly communicate the intended operation.

A typical approach is:

| Method | Typical purpose |
|---|---|
| GET | Retrieve information |
| POST | Create a resource or submit an operation |
| PUT | Replace a resource |
| PATCH | Partially update a resource |
| DELETE | Delete a resource |

The exact API design may vary, but the important point is to use conventions consistently.

If similar operations behave differently across an API, developers have to learn exceptions instead of being able to rely on predictable patterns.

## 5. Give parameters meaningful names

Parameters should be easy to understand without requiring additional investigation.

A well-defined parameter should normally have:

- A meaningful name
- A data type
- A clear description
- An indication of whether it is required
- A default value, where applicable
- Any relevant constraints

For example:

| Parameter | Type | Required | Default | Description |
|---|---|---:|---|---|
| `customer_id` | string | Yes | — | Identifier of the customer |
| `limit` | integer | No | 10 | Maximum number of results to return |
| `include_history` | boolean | No | false | Includes historical information |

`customer_id` provides more context than simply calling the parameter `id`, especially in an API that works with several types of resources.

## 6. Make required and optional parameters explicit

Developers should not have to guess which parameters are mandatory.

For example:

| Parameter | Required | Default |
|---|---:|---|
| `customer_id` | Yes | — |
| `limit` | No | 10 |
| `include_history` | No | false |

This makes the API contract easier to understand.

Defaults are also important because they define what happens when an optional parameter is omitted.

If a parameter has a default value, that behaviour should be documented clearly.

## 7. Define constraints

A parameter description is not always enough.

Where relevant, define constraints such as:

- Allowed values
- Minimum and maximum values
- Length restrictions
- Formatting requirements
- Whether values can be combined
- Dependencies between parameters

For example:

| Parameter | Constraint |
|---|---|
| `limit` | Integer between 1 and 100 |
| `status` | `active`, `inactive` or `pending` |
| `customer_id` | Required identifier |

Constraints help consumers construct valid requests and reduce avoidable errors.

If a constraint is not known or documented, it should not be invented.

## 8. Make responses predictable

A successful response should have a clear and consistent structure.

For example:

    response
    ├── data
    ├── metadata
    └── errors

The exact structure will depend on the API, but related endpoints should use consistent conventions where possible.

Predictable responses make APIs easier to learn and integrate with.

They also make documentation easier to structure because similar concepts can be explained in similar ways.

## 9. Treat errors as part of the API contract

Errors are part of the API, not an afterthought.

Documentation should explain, where the information is available:

- HTTP status
- Meaning of the error
- Conditions that cause it
- Relevant response information
- What the consumer can do next

For example:

### 400 Bad Request

A `400 Bad Request` response can indicate that the request contains an invalid parameter or does not satisfy the documented request requirements.

The exact cause should be documented according to the behaviour of the API.

Good error documentation helps developers determine whether they need to change their request or investigate a problem elsewhere.

## 10. Design examples as carefully as the API

Examples are often the quickest way for a developer to understand how an API works.

A useful example should:

- Use realistic but safe values
- Match the documented parameter names
- Use the correct endpoint and HTTP method
- Reflect the documented response structure
- Clearly identify placeholders
- Avoid unnecessary complexity

Examples should be reviewed against the API definition.

An example that contradicts the reference documentation can be more confusing than having no example at all.

## 11. Design with documentation in mind

API design and API documentation should not be treated as completely separate activities.

A well-designed API is easier to explain because its behaviour is clear and consistent.

Documentation should normally make it possible for a developer to answer questions such as:

- What does this API do?
- Which endpoint should I use?
- Which parameters do I need?
- What values are allowed?
- What happens if I omit an optional parameter?
- What does a successful response look like?
- What errors can occur?
- Can I see a complete example?

If these questions are difficult to answer, the problem may not be documentation alone. It may indicate that the API itself needs clarification.

## 12. Separate reference information from task-oriented guidance

Reference documentation and tutorials serve different purposes.

### Reference documentation

Reference documentation answers:

> What does the API contain?

It provides detailed information about endpoints, parameters, data types, responses and errors.

### Tutorial or task-oriented documentation

A tutorial answers:

> How do I use the API to accomplish a task?

It guides the reader through a sequence of steps.

Both can be useful.

The reference provides precision and completeness.

The tutorial provides context and helps the reader get started.

## 13. Do not document assumptions

One of the most important principles in technical documentation is to distinguish between what is known and what is assumed.

For example, if the available source material does not document:

- Authentication
- Base URL
- Request headers
- Rate limits
- Additional parameter constraints

these should not simply be filled in with plausible information.

They should be identified as gaps requiring clarification or additional source material.

This is particularly important when AI is used to assist with documentation.

AI can produce technically convincing content that is not supported by the source.

The documentation process therefore needs a clear boundary between:

    Documented information
            ↓
    Can be documented directly

    Missing information
            ↓
    Requires clarification

    Ambiguous information
            ↓
    Requires human review

## 14. Use AI to support the process

AI can be useful at several stages of API documentation and analysis.

For example, it can help to:

- Extract information from source material
- Identify parameters and response elements
- Structure technical information
- Compare documentation with source material
- Identify potential omissions
- Flag inconsistent terminology
- Review examples
- Identify possible contradictions
- Suggest clearer wording

However, AI should not be treated as the technical authority.

A controlled workflow might look like this:

    Source material
          ↓
    Content analysis
          ↓
    Structured information
          ↓
    Documentation draft
          ↓
    AI-assisted review
          ↓
    Human validation
          ↓
    Publication

The source material and appropriate technical stakeholders remain the basis for determining technical accuracy.

## 15. Consider maintainability from the beginning

An API is likely to change over time.

Parameters may be added or removed. Response structures may evolve. Defaults may change. New versions may be introduced.

Documentation therefore needs to be maintainable.

Useful practices include:

- Clear versioning
- Consistent terminology
- Structured parameter information
- Clear ownership
- Traceability to source information
- Review processes
- Defined quality checks

Good documentation is not simply accurate when it is first published. It should also be possible to update it when the API changes.

## 16. Review the API and its documentation together

Before publication, both the API design and its documentation should be reviewed.

### API design checklist

    [ ] The intended use case is clear
    [ ] Requirements have been identified
    [ ] Resources are named consistently
    [ ] HTTP methods are used consistently
    [ ] Parameters have meaningful names
    [ ] Data types are defined
    [ ] Required and optional parameters are clear
    [ ] Defaults are documented
    [ ] Constraints are defined where applicable
    [ ] Response structures are predictable
    [ ] Error behaviour is defined
    [ ] Examples reflect the API

### Documentation checklist

    [ ] API purpose is clear
    [ ] Endpoint and method are documented
    [ ] Parameters are documented
    [ ] Data types are documented
    [ ] Required and optional values are clear
    [ ] Defaults are documented
    [ ] Constraints are documented where available
    [ ] Request examples are accurate
    [ ] Response examples are accurate
    [ ] Errors are documented
    [ ] Terminology is consistent
    [ ] Undocumented behaviour has not been invented
    [ ] Documentation has been reviewed against the source

## Conclusion

Better API design is not only about technical implementation.

It is about creating a clear and predictable contract between the API and the people or systems that consume it.

The process can be viewed as:

    Understand the use case
             ↓
    Define the requirements
             ↓
    Design the API
             ↓
    Document the contract
             ↓
    Review and validate
             ↓
    Maintain as the API evolves

From a documentation perspective, good API design makes the technical information easier to understand, structure and maintain.

From a requirements perspective, it provides a clearer connection between what the user needs and what the system delivers.

The result is an API that is not only functional, but easier to **understand, integrate and maintain**.

## Related Work

This article is part of my technical documentation portfolio.

Related examples include:

- API reference documentation
- API tutorials
- Configuration documentation
- AI-assisted documentation workflows
- Requirements and information analysis

## Portfolio Note

This article is a portfolio piece demonstrating practical thinking around API usability, requirements, technical documentation and AI-assisted documentation workflows.
