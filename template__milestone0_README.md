# Template README for BINF 503 Project

## Open on GitHub: [template\_\_README.md](https://github.com/nourgaser-giu/giu-bi-ebd-w2025/blob/main/template__milestone0_README.md)

## Download (ctrl+s to save): [template\_\_README.md](https://raw.githubusercontent.com/nourgaser-giu/giu-bi-ebd-w2025/main/template__milestone0_README.md)

# CYBERVISTA

**Course:** Electronic Business Development (BINF 503)  
**Semester:** Winter 2025  
**Instructor:** Dr. Nourhan Hamdi  
**Teaching Assistants:** Mr. Nour Gaser, Mr. Omar Alaa

CyberVista: A Cyber-Assurance Platform for Fintech

1. Team Members

Name                 	Student ID	                       Tutorial Group                           	GitHub Username
Nathalie Romani       	13003489	                        02	                                      nathalieromani
Mariam Ali             	13003733	                        02	                                     
Mohamed Adel	          13002518	                        02	                                       
Adam el sheribini     	13002519                         	02	                                       
Maria Ramy            	13007233                        	04                                       	mariaramynabil
Mohamed Amgad 	        13001125	                        05	                                       MoamgadMo-art

2. Project Description
Concept: CyberVista is a SaaS (Software-as-a-Service) platform that provides automated cyber-assurance services to fintech companies and startups. We solve the problem of high costs and complexity associated with achieving and maintaining cybersecurity compliance and risk management. Our platform offers streamlined security scoring, compliance readiness checks, and continuous monitoring through a centralized dashboard, enabling fintech to build trust with partners and customers more efficiently.
• Concept: An e-business platform delivering essential cybersecurity and compliance services tailored for the fintech industry.
• Link to Fin-Tech Course Document: 



3. Feature Breakdown
   
3.1 Full Scope

List ALL potential features/user stories envisioned for the complete product (beyond just this course).
• Automated Security Scoring: Generate a quantifiable security score for a fintech company based on a questionnaire and system scans.
• Compliance Dashboard: A central hub displaying compliance status against standards like PCI-DSS, ISO 27001, and GDPR.
• Compliance Readiness Modules: Interactive checklists and guides for specific financial regulations.
• Vulnerability Assessment Tool: A simplified scanner to identify common security weaknesses in web applications.
• Fraud Risk Analytics: Analyze transaction patterns to flag potential fraudulent activities.
• Digital Identity Verification Log: A secure log to track and assess the risks associated with user identity verification processes.
• Audit Report Generation: Automatically generate compliance and security reports for internal or external auditors.
• Real-time Security Alerts: Notify users of critical security events or compliance failures.
• Vendor Risk Management: Assess and monitor the cybersecurity posture of third-party vendors.



3.2 Selected MVP Use Cases (Course Scope)
From the list above, identify the 5 or 6 specific use cases you will implement for this course. Note: User Authentication is mandatory.
1.	User Authentication (Registration/Login for Fintech Companies)
2.	Company Profile & Security Questionnaire: Onboard a company and collect initial data via a security questionnaire.
3.	Compliance Dashboard: Display a summary view of the company's overall security score and compliance status.
4.	Vulnerability Assessment Tool: Allow users to submit their website URL for a basic, automated security scan.
5.	Audit Report Generation: Enable users to generate a downloadable PDF report summarizing their security posture and questionnaire answers.
6.	Security Alert Inbox: A simple inbox within the dashboard to receive and view system-generated security alerts.

 
 4. Feature Assignments (Accountability)
	Assign one distinct use case from Section 3.2 to each team member. This member is responsible for the full-stack implementation of this feature.
Team Member            	Assigned Use Case	                   Brief Description of Responsibility
Maria           	User Authentication	                       Register, Login, JWT handling, Password Hashing for company accounts.
Mariam 	          Company Profile & Security Questionnaire	   Create and manage company profile; design, serve, and store questionnaire responses.
Nathalie 	         Compliance Dashboard	                      Front-end dashboard UI; back-end logic to calculate/retrieve security score and status.
Amgad 	            Vulnerability Assessment Tool	          Interface to submit a URL; integrate with a simple scanning API; display scan results.
Mohamed           	Audit Report Generation                	Backend logic to compile data (profile, questionnaire, scan results) into a structured PDF report.
Adam           	    Security Alert Inbox                    	Database model for alerts; backend API to create/manage alerts; front-end inbox UI.

5. Data Model (Initial Schemas)
Define the initial Mongoose Schemas for your application's main data models (User, Transaction, Account, etc.). You may use code blocks or pseudo-code.
User Schema

javascript
const UserSchema = new mongoose.Schema({
    companyName: { type: String, required: true },
    email: { type: String, required: true, unique: true },
    password: { type: String, required: true },
    industry: { type: String },
    dateRegistered: { type: Date, default: Date.now }
});
CompanyProfile Schema
javascript
const CompanyProfileSchema = new mongoose.Schema({
    userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
    securityQuestionnaire: {
        dataEncryption: { type: Boolean },
        hasIncidentResponse: { type: Boolean },
        // ... other questionnaire fields
    },
    overallSecurityScore: { type: Number, min: 0, max: 100 },
    lastAssessmentDate: { type: Date }
});
VulnerabilityScan Schema
javascript
const VulnerabilityScanSchema = new mongoose.Schema({
    userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
    targetUrl: { type: String, required: true },
    scanDate: { type: Date, default: Date.now },
    status: { type: String, enum: ['Pending', 'Completed', 'Failed'], default: 'Pending' },
    results: { type: Object } // Could store findings like { "high": 2, "medium": 5, "low": 1 }
});
SecurityAlert Schema
javascript
const SecurityAlertSchema = new mongoose.Schema({
    userId: { type: mongoose.Schema.Types.ObjectId, ref: 'User', required: true },
    title: { type: String, required: true },
    message: { type: String, required: true },
    alertLevel: { type: String, enum: ['Low', 'Medium', 'High', 'Critical'] },
    dateGenerated: { type: Date, default: Date.now },
    isRead: { type: Boolean, default: false }
});



