# NuData Tree Nodes

This integration provides administrators with the ability to include the NuData Javascript SDK, retrieve the risk NuData Score, provide and the authentication outcome within authentication journeys:

* [NuData Behavior Solutions](https://b2b.mastercard.com/identity/behavioral-solutions)
## Compatibility


You can implement this node on the following systems:

| Product | Compatible? |
|----------|--------------|
| ForgeRock Identity Cloud | Yes |
| ForgeRock Access Management (self-managed) | Yes |
| ForgeRock Identity Platform (self-managed) | Yes |

## NuData Initialize

Initialize the NuData SDK on a Page Node, using the configuration provided by the node properties.

### Inputs

No external inputs required.

### Configuration

| Property | Usage |
|-----------|--------|
| Base URL | The NuData SDK Base URL |
| Client ID | The NuData Client ID |
| NuData SDK Version | The NuData SDK Version |

### Outputs

- `nuDataWidgetData` – The NuData behavioral data collected.

### Outcomes

- `Next` – The NuData SDK was successfully initialized and the NuData widget data was collected.  
- `Error` – An error occurred during the NuData SDK initialization process.

## NuData Score

Submits the NuData collected behavioral data and returns the NuData risk level and other risk-related details associated with an event.

### Compatibility

| Product | Compatible? |
|----------|--------------|
| ForgeRock Identity Cloud | Yes |
| ForgeRock Access Management (self-managed) | Yes |
| ForgeRock Identity Platform (self-managed) | No |

### Inputs

This node retrieves `nuDataWidgetData` from the journey state.

### Configuration

| Property | Usage |
|-----------|--------|
| Client Name | The NuData Client Name |
| SDK Version | The NuData SDK Version |
| Client Key | The NuData Client Key |
| Placement Name | The NuData Placement Name |
| Placement Type | The NuData Placement Type (Login, Forgot Username, Reset Password, Change Password) |
| Page Placement Number | The NuData Page Placement Number |
| Placement Outcome | The Placement Outcome of the branch in the Journey |

### Outputs

- `nuDataScoreResponse` – The NuData score and other risk analysis data.

### Outcomes

- `Red` – The Red outcome indicates the highest risk score returned from NuData.  
- `Yellow` – The Yellow outcome indicates a medium risk score returned from NuData.  
- `Green` – The Green outcome indicates the lowest risk score returned from NuData.  
- `Error` – An error occurred during the retrieval of the NuData Score process.

## NuData Trigger MFA

The NuData Trigger MFA node is a helper node that checks the NuData Score response to determine if the `mfa_signal` value was returned.

### Compatibility

| Product | Compatible? |
|----------|--------------|
| ForgeRock Identity Cloud | Yes |
| ForgeRock Access Management (self-managed) | Yes |
| ForgeRock Identity Platform (self-managed) | No |

### Inputs

This node retrieves `nuDataScoreResponse` from the journey state.

### Configuration

None

### Outputs

None

### Outcomes

- `Trigger MFA` – The `mfa_signal` value was detected in the NuData score response, indicating MFA should be triggered.  
- `Next` – Continue to the next node in the Journey.  
- `Error` – An error occurred during the NuData SDK initialization process.

## NuData Update

Submits the NuData collected behavioral data and the final Placement outcome.

### Compatibility

| Product | Compatible? |
|----------|--------------|
| ForgeRock Identity Cloud | Yes |
| ForgeRock Access Management (self-managed) | Yes |
| ForgeRock Identity Platform (self-managed) | No |

### Inputs

This node retrieves `nuDataWidgetData` from the journey state.

### Configuration

| Property | Usage |
|-----------|--------|
| Client Name | The NuData Client Name |
| SDK Version | The NuData SDK Version |
| Client Key | The NuData Client Key |
| Placement Name | The NuData Placement Name |
| Placement Type | The NuData Placement Type (Login, Forgot Username, Reset Password, Change Password) |
| Page Placement Number | The NuData Page Placement Number |
| Placement Outcome | The Placement Outcome of the branch in the Journey |

### Outputs

- `nuDataUpdateResponse` – The NuData update response.

### Outcomes

- `Next` – The NuData update was successful; proceed to the next step in the Journey.  
- `Error` – An error occurred during the retrieval of the NuData Score process.

## Troubleshooting

If this node logs an error, review the log messages to find the reason for the error and address the issue appropriately.

## Support

If you encounter any issues, be sure to check our **[Troubleshooting](https://backstage.forgerock.com/knowledge/kb/article/a68547609)** pages.

Support tickets can be raised whenever you need our assistance; here are some examples of when it is appropriate to open a ticket (but not limited to):

* Suspected bugs or problems with Ping Identity software.
* Requests for assistance

You can raise a ticket using **[BackStage](https://backstage.forgerock.com/support/tickets)**, our customer support portal that provides one stop access to Ping Identity services.

BackStage shows all currently open support tickets and allows you to raise a new one by clicking **New Ticket**.