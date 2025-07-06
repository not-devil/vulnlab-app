# 🔓 VulnLab - PHP Web Application

A deliberately vulnerable web application built with HTML, CSS, JavaScript, PHP, and MySQL for educational purposes. This application is designed to help security professionals and students practice identifying and exploiting common web vulnerabilities.

## ⚠️ Security Warning

**This application contains intentional security vulnerabilities and should NEVER be deployed in a production environment or on systems connected to sensitive networks.**

## 🎯 Purpose

This application serves as a practice platform for:
- Web application security testing
- Penetration testing techniques
- Vulnerability assessment
- Security awareness training
- Learning secure coding practices

## 🛠️ Technologies Used

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Backend**: PHP 7.4+
- **Database**: MySQL 8.0+
- **Web Server**: Apache 2.4+

## 📋 Prerequisites

Before running this application, ensure you have the following installed:

- **XAMPP/WAMP/LAMP** stack or individual components:
  - Apache Web Server 2.4+
  - PHP 7.4 or higher
  - MySQL 8.0 or higher
- **Git** (for cloning the repository)
- **Web Browser** (Chrome, Firefox, Safari, Edge)

## 🚀 Installation & Setup

### Option 1: Using XAMPP (Recommended for beginners)

1. **Download and Install XAMPP**
   ```bash
   # Download from: https://www.apachefriends.org/download.html
   # Install following the setup wizard
   ```

2. **Clone the Repository**
   ```bash
   git clone https://github.com/yourusername/vulnlab-php.git
   cd vulnlab-php
   ```

3. **Move to Web Directory**
   ```bash
   # Copy the project to XAMPP htdocs folder
   cp -r vulnlab-php /opt/lampp/htdocs/
   # Or on Windows: copy to C:\xampp\htdocs\
   ```

4. **Start XAMPP Services**
   ```bash
   sudo /opt/lampp/lampp start
   # Or use XAMPP Control Panel on Windows
   ```

5. **Setup Database**
   - Open phpMyAdmin: http://localhost/phpmyadmin
   - Create a new database named `vulnlab`
   - Import the database schema: `database/vulnlab.sql`

6. **Configure Database Connection**
   ```bash
   # Edit config/database.php with your database credentials
   cp config/database.example.php config/database.php
   ```

7. **Access the Application**
   - Open your browser and navigate to: http://localhost/vulnlab-php

### Option 2: Manual Installation

1. **Install Apache, PHP, and MySQL**
   ```bash
   # Ubuntu/Debian
   sudo apt update
   sudo apt install apache2 php php-mysql mysql-server
   
   # CentOS/RHEL
   sudo yum install httpd php php-mysql mysql-server
   
   # macOS (using Homebrew)
   brew install httpd php mysql
   ```

2. **Clone and Configure**
   ```bash
   git clone https://github.com/yourusername/vulnlab-php.git
   sudo cp -r vulnlab-php /var/www/html/
   sudo chown -R www-data:www-data /var/www/html/vulnlab-php
   ```

3. **Database Setup**
   ```bash
   mysql -u root -p
   CREATE DATABASE vulnlab;
   USE vulnlab;
   SOURCE /var/www/html/vulnlab-php/database/vulnlab.sql;
   ```

4. **Configure PHP**
   ```bash
   # Edit /etc/php/7.4/apache2/php.ini
   # Ensure these settings for vulnerability testing:
   display_errors = On
   display_startup_errors = On
   error_reporting = E_ALL
   ```

5. **Restart Services**
   ```bash
   sudo systemctl restart apache2
   sudo systemctl restart mysql
   ```

## 📁 Project Structure

```
vulnlab-php/
├── README.md
├── index.php
├── config/
│   ├── database.php
│   ├── database.example.php
│   └── config.php
├── includes/
│   ├── header.php
│   ├── footer.php
│   ├── navigation.php
│   └── functions.php
├── modules/
│   ├── xss/
│   │   ├── reflected.php
│   │   ├── stored.php
│   │   └── dom.php
│   ├── sqli/
│   │   ├── union.php
│   │   ├── blind.php
│   │   └── error.php
│   ├── csrf/
│   │   ├── transfer.php
│   │   └── profile.php
│   └── upload/
│       ├── upload.php
│       └── uploads/
├── assets/
│   ├── css/
│   │   ├── style.css
│   │   └── bootstrap.min.css
│   ├── js/
│   │   ├── main.js
│   │   └── jquery.min.js
│   └── images/
│       ├── logo.png
│       └── icons/
├── database/
│   ├── vulnlab.sql
│   ├── schema.sql
│   └── sample_data.sql
├── admin/
│   ├── index.php
│   ├── users.php
│   └── logs.php
├── api/
│   ├── users.php
│   ├── comments.php
│   └── search.php
├── docs/
│   ├── installation.md
│   ├── vulnerabilities.md
│   └── api-docs.md
├── logs/
│   ├── access.log
│   └── error.log
└── .htaccess
```

## 🎯 Available Vulnerabilities

### 1. Cross-Site Scripting (XSS)
- **Reflected XSS**: `/modules/xss/reflected.php`
- **Stored XSS**: `/modules/xss/stored.php`
- **DOM XSS**: `/modules/xss/dom.php`

### 2. SQL Injection
- **Union-based**: `/modules/sqli/union.php`
- **Blind SQLi**: `/modules/sqli/blind.php`
- **Error-based**: `/modules/sqli/error.php`

### 3. Cross-Site Request Forgery (CSRF)
- **Fund Transfer**: `/modules/csrf/transfer.php`
- **Profile Update**: `/modules/csrf/profile.php`

### 4. File Upload Vulnerabilities
- **Unrestricted Upload**: `/modules/upload/upload.php`

### 5. Additional Vulnerabilities
- **Path Traversal**
- **Command Injection**
- **Session Management Issues**
- **Authentication Bypass**

## 🔧 Configuration

### Database Configuration
Edit `config/database.php`:
```php
<?php
$host = 'localhost';
$username = 'root';
$password = '';
$database = 'vulnlab';
$port = 3306;
?>
```

### Security Levels
The application supports different difficulty levels:
- **Low**: Basic vulnerabilities, minimal filtering
- **Medium**: Some filtering, bypassable protections
- **High**: Advanced filtering, realistic scenarios

## 🧪 Testing Guidelines

### Sample Payloads

**XSS Testing:**
```javascript
<script>alert('XSS')</script>
<img src=x onerror=alert('XSS')>
<svg onload=alert('XSS')>
```

**SQL Injection Testing:**
```sql
' OR 1=1 --
' UNION SELECT 1,2,3 --
' AND (SELECT COUNT(*) FROM users) > 0 --
```

**CSRF Testing:**
```html
<form action="http://localhost/vulnlab-php/modules/csrf/transfer.php" method="POST">
  <input type="hidden" name="amount" value="1000">
  <input type="hidden" name="account" value="attacker">
  <input type="submit" value="Click me">
</form>
```

## 🛡️ Security Best Practices (What NOT to do)

This application demonstrates what NOT to do in production:
- ❌ No input validation
- ❌ No output encoding
- ❌ No parameterized queries
- ❌ No CSRF tokens
- ❌ No file upload restrictions
- ❌ No authentication checks
- ❌ No session security

## 📚 Learning Resources

- [OWASP Top 10](https://owasp.org/www-project-top-ten/)
- [OWASP Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [PHP Security Guide](https://phpsecurity.readthedocs.io/)
- [SQL Injection Prevention](https://cheatsheetseries.owasp.org/cheatsheets/SQL_Injection_Prevention_Cheat_Sheet.html)

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/new-vulnerability`
3. Commit your changes: `git commit -am 'Add new vulnerability'`
4. Push to the branch: `git push origin feature/new-vulnerability`
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## ⚠️ Disclaimer

This application is for educational purposes only. The developers are not responsible for any misuse of this application. Always obtain proper authorization before testing on systems you do not own.

## 🐛 Known Issues

- Application is intentionally vulnerable
- No security headers implemented
- Logging may contain sensitive information
- Error messages may reveal system information

## 📞 Support

For questions or issues:
- Create an issue on GitHub
- Check the documentation in `/docs/`
- Review the troubleshooting guide

## 🚀 Deployment Notes

**DO NOT DEPLOY IN PRODUCTION**

For educational deployment:
1. Use isolated networks
2. Implement proper firewall rules
3. Regular backup of test data
4. Monitor for unexpected usage

---

**Remember: This is a vulnerable application by design. Use responsibly and only in controlled environments.**
