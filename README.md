# Freshservice MCP Server
[![smithery badge](https://smithery.ai/badge/@effytech/freshservice_mcp)](https://smithery.ai/server/@effytech/freshservice_mcp)

An MCP server implementation that integrates with Freshservice, enabling AI models to interact with Freshservice modules and perform various support operations.

## Features

- **Freshservice Integration**: Seamless interaction with Freshservice API endpoints
- **AI Model Support**: Enables AI models to perform support operations through Freshservice
- **Automated Ticket Management**: Handle ticket creation, updates, and responses

## Components

### Tools

The server offers several tools for Freshservice operations:

- `create_ticket`: Create new support tickets
  - **Inputs**:
    - `subject` (string, required): Ticket subject
    - `description` (string, required): Ticket description
    - `source` (number, required): Ticket source code
    - `priority` (number, required): Ticket priority level
    - `status` (number, required): Ticket status code
    - `email` (string, optional): Email of the requester
    - `requester_id` (number, optional): ID of the requester
    - `custom_fields` (object, optional): Custom fields to set on the ticket
    - `additional_fields` (object, optional): Additional top-level fields

- `update_ticket`: Update existing tickets
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket to update
    - `ticket_fields` (object, required): Fields to update

- `delete_ticket`: Delete a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket to delete

- `search_tickets`: Search for tickets based on criteria
  - **Inputs**:
    - `query` (string, required): Search query string

- `get_ticket_fields`: Get all ticket fields
  - **Inputs**:
    - None

- `get_tickets`: Get all tickets
  - **Inputs**:
    - `page` (number, optional): Page number to fetch
    - `per_page` (number, optional): Number of tickets per page

- `get_ticket`: Get a single ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket to get

- `get_ticket_conversation`: Get conversation for a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket

- `create_ticket_reply`: Reply to a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket
    - `body` (string, required): Content of the reply

- `create_ticket_note`: Add a note to a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket
    - `body` (string, required): Content of the note

- `update_ticket_conversation`: Update a conversation
  - **Inputs**:
    - `conversation_id` (number, required): ID of the conversation
    - `body` (string, required): Updated content

- `view_ticket_summary`: Get the summary of a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket

- `update_ticket_summary`: Update the summary of a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket
    - `body` (string, required): New summary content

- `delete_ticket_summary`: Delete the summary of a ticket
  - **Inputs**:
    - `ticket_id` (number, required): ID of the ticket

- `get_agents`: Get all agents
  - **Inputs**:
    - `page` (number, optional): Page number
    - `per_page` (number, optional): Number of agents per page

- `view_agent`: Get a single agent
  - **Inputs**:
    - `agent_id` (number, required): ID of the agent

- `create_agent`: Create a new agent
  - **Inputs**:
    - `agent_fields` (object, required): Agent details

- `update_agent`: Update an agent
  - **Inputs**:
    - `agent_id` (number, required): ID of the agent
    - `agent_fields` (object, required): Fields to update

- `search_agents`: Search for agents
  - **Inputs**:
    - `query` (string, required): Search query

- `list_contacts`: Get all contacts
  - **Inputs**:
    - `page` (number, optional): Page number
    - `per_page` (number, optional): Contacts per page

- `get_contact`: Get a single contact
  - **Inputs**:
    - `contact_id` (number, required): ID of the contact

- `search_contacts`: Search for contacts
  - **Inputs**:
    - `query` (string, required): Search query

- `update_contact`: Update a contact
  - **Inputs**:
    - `contact_id` (number, required): ID of the contact
    - `contact_fields` (object, required): Fields to update

- `list_companies`: Get all companies
  - **Inputs**:
    - `page` (number, optional): Page number
    - `per_page` (number, optional): Companies per page

- `view_company`: Get a single company
  - **Inputs**:
    - `company_id` (number, required): ID of the company

- `search_companies`: Search for companies
  - **Inputs**:
    - `query` (string, required): Search query

- `find_company_by_name`: Find a company by name
  - **Inputs**:
    - `name` (string, required): Company name

- `list_company_fields`: Get all company fields
  - **Inputs**:
    - None

## Getting Started

### Installing via Smithery

To install freshservice_mcp for Claude Desktop automatically via [Smithery](https://smithery.ai/server/@effytech/freshservice_mcp):

```bash
npx -y @smithery/cli install @effytech/freshservice_mcp --client claude
```

### Prerequisites

- A Freshservice account (sign up at [freshservice.com](https://freshservice.com))
- Freshservice API key
- `uvx` installed (`pip install uv` or `brew install uv`)

### Configuration

1. Generate your Freshservice API key from the Freshservice admin panel
2. Set up your domain and authentication details

### Usage with Claude Desktop

1. Install Claude Desktop if you haven't already
2. Add the following configuration to your `claude_desktop_config.json`:

```json
"mcpServers": {
  "freshservice-mcp": {
    "command": "uvx",
    "args": [
        "freshservice-mcp"
    ],
    "env": {
      "FRESHSERVICE_API_KEY": "<YOUR_FRESHSERVICE_API_KEY>",
      "FRESHSERVICE_DOMAIN": "<YOUR_FRESHSERVICE_DOMAIN>"
    }
  }
}
```

**Important Notes**:
- Replace `YOUR_FRESHSERVICE_API_KEY` with your actual Freshservice API key
- Replace `YOUR_FRESHSERVICE_DOMAIN` with your Freshservice domain (e.g., `yourcompany.freshservice.com`)

## Example Operations

Once configured, you can ask Claude to perform operations like:

- "Create a new ticket with subject 'Payment Issue for customer A101' and description as 'Reaching out for a payment issue in the last month for customer A101', where customer email is a101@acme.com and set priority to high"
- "Update the status of ticket #12345 to 'Resolved'"
- "List all high-priority tickets assigned to the agent John Doe"
- "List previous tickets of customer A101 in last 30 days"


## Testing

For testing purposes, you can start the server manually:

```bash
uvx freshservice-mcp --env FRESHSERVICE_API_KEY=<your_api_key> --env FRESHSERVICE_DOMAIN=<your_domain>
```

## Troubleshooting

- Verify your Freshservice API key and domain are correct
- Ensure proper network connectivity to Freshservice servers
- Check API rate limits and quotas
- Verify the `uvx` command is available in your PATH

## License

This MCP server is licensed under the MIT License. See the LICENSE file in the project repository for full details.
