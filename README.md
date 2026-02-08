# Bulk Email Dispatcher

A simple and efficient bulk email dispatcher built with TypeScript, Node.js, and npm. This application allows you to send personalized HTML emails to multiple recipients using an SMTP server.

## Features

- Send personalized HTML emails to multiple recipients
- Template support using Mustache for dynamic content
- CSV-based recipient management
- Environment variable configuration for secure SMTP settings
- Built with TypeScript for type safety

## Prerequisites

- Node.js (v14 or higher)
- npm (v6 or higher)
- An SMTP email account (e.g., Gmail, Outlook, etc.)

## Setup

### 1. Clone or Download the Repository

```bash
git clone https://github.com/your-username/bulk-email-dispatcher.git
cd bulk-email-dispatcher
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory and add your SMTP credentials:

```env
MAIL_HOST=smtp.your-email-provider.com
EMAIL_USER=your-email@domain.com
EMAIL_PASSWORD=your-app-password
FROM_NAME=Your Name
```

**Note**: For Gmail, you'll need to use an App Password instead of your regular password. Follow Google's guide on how to create an App Password.

### 4. Prepare Recipients List

Create a CSV file named `email-recipients.csv` in the root directory with the following format:

```csv
email,name
recipient1@example.com,John Doe
recipient2@example.com,Jane Smith
```

The first column should be the email address, and the second column should be the recipient's name for personalization.

### 5. Customize Email Template

Edit the `email-template.html` file to customize your email content. You can use Mustache-style variables like `{{name}}` to personalize the email content for each recipient.

Example template:

```html
<!DOCTYPE html>
<html>
<head>
  <title>Your Email Subject</title>
</head>
<body>
  <p>Dear {{name}},</p>
  <p>Your personalized message here.</p>
</body>
</html>
```

## Usage

### Compile and Run

To compile and run the application:

```bash
npm start
```

This command will:
1. Compile the TypeScript code to JavaScript
2. Execute the compiled code with Node.js
3. Send emails to all recipients in your CSV file

### Development

To compile the TypeScript code without running:

```bash
npx tsc
```

The compiled JavaScript files will be placed in the `dist` directory.

## Project Structure

```
bulk-email-dispatcher/
├── src/
│   └── index.ts          # Main application file
├── dist/                 # Compiled JavaScript files
├── email-template.html   # HTML email template
├── email-recipients.csv  # Recipient list
├── .env                  # Environment variables (not committed)
├── .gitignore           # Git ignore rules
├── package.json         # Project dependencies and scripts
├── tsconfig.json        # TypeScript configuration
└── README.md           # This file
```

## Security Considerations

- Never commit your `.env` file to version control
- Use strong passwords and App Passwords where required
- Limit the number of emails sent per hour/day based on your SMTP provider's limits
- Consider using a dedicated SMTP service for large volumes (e.g., SendGrid, Amazon SES)

## Customization

### Changing Input Files

To change the CSV or HTML template file names, modify the call at the bottom of `src/index.ts`:

```ts
(async () => sendMail(`./your-custom-recipients.csv`, `your-custom-template.html`))();
```

### Adding More Personalization Variables

Add more columns to your CSV file and corresponding variables in your HTML template:

CSV:
```csv
email,name,location
john@example.com,John Doe,New York
jane@example.com,Jane Smith,Los Angeles
```

Template:
```html
<p>Dear {{name}} from {{location}},</p>
```

## Troubleshooting

### Common Issues

1. **Authentication Error**: Check your email credentials and ensure you're using an App Password if using Gmail
2. **Connection Timeout**: Verify your MAIL_HOST setting and check firewall settings
3. **Emails Going to Spam**: Ensure your SMTP settings comply with the provider's requirements and consider adding proper headers

### Enable Logging

For debugging purposes, you can add console.log statements to see the email sending progress in the application output.

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the ISC License - see the LICENSE file for details.

## Acknowledgments

- [Nodemailer](https://nodemailer.com/) for email sending capabilities
- [Mustache](https://github.com/janl/mustache.js/) for templating
- [Dotenv](https://github.com/motdotla/dotenv) for environment variable management
