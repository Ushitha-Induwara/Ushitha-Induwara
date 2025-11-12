# Google Maps Web Application

A simple Java EE web application that displays an interactive Google Map using Maven, Java Servlets, and the Google Maps JavaScript API.

## 🌍 Overview

This project demonstrates a basic Java web application that integrates Google Maps to display a map centered on **Colombo, Sri Lanka** with a marker at the specified location.

## 🚀 Features

- **Full-screen Google Map** display
- **Centered on Colombo, Sri Lanka** (Latitude: 6.9271, Longitude: 79.8612)
- **Custom marker** at the center location
- **Responsive design** that works on all screen sizes
- **Maven-based** build system
- **Ready for deployment** on Apache Tomcat

## 📋 Prerequisites

- **Java Development Kit (JDK)** 11 or higher
- **Apache Maven** 3.6 or higher
- **Apache Tomcat** 9.x or 10.x
- **IntelliJ IDEA** (Community or Ultimate Edition)
- **Google Maps API Key** ([Get one here](https://developers.google.com/maps/documentation/javascript/get-api-key))

## 🏗️ Project Structure

```
google-maps-webapp/
├── pom.xml                                 # Maven configuration
├── src/
│   └── main/
│       ├── java/
│       │   └── com/example/map/
│       │       └── MapServlet.java         # Main servlet
│       └── webapp/
│           ├── WEB-INF/
│           │   └── web.xml                 # Web deployment descriptor
│           └── index.html                  # Frontend HTML page
├── .gitignore                              # Git ignore file
├── SETUP_GUIDE.md                          # Detailed setup instructions
└── PROJECT_README.md                       # This file
```

## ⚙️ Technology Stack

| Component | Technology |
|-----------|-----------|
| Backend | Java Servlets (Jakarta EE) |
| Frontend | HTML5, CSS3, JavaScript |
| API | Google Maps JavaScript API |
| Build Tool | Apache Maven |
| Server | Apache Tomcat |
| IDE | IntelliJ IDEA |

## 🔧 Quick Start

### 1. Configure Google Maps API Key

Open `src/main/webapp/index.html` and replace the placeholder with your actual API key:

```html
<script async defer
    src="https://maps.googleapis.com/maps/api/js?key=YOUR_ACTUAL_API_KEY&callback=initMap">
</script>
```

### 2. Build the Project

```bash
mvn clean package
```

This will generate `target/google-maps-webapp.war`

### 3. Deploy to Tomcat

**Option A: Using IntelliJ IDEA**
- See detailed instructions in [SETUP_GUIDE.md](SETUP_GUIDE.md)

**Option B: Manual Deployment**
```bash
# Copy WAR to Tomcat webapps directory
cp target/google-maps-webapp.war /path/to/tomcat/webapps/

# Start Tomcat
/path/to/tomcat/bin/startup.sh  # Linux/Mac
# or
/path/to/tomcat/bin/startup.bat # Windows
```

### 4. Access the Application

Navigate to: `http://localhost:8080/google-maps-webapp/`

## 📖 Detailed Setup Guide

For comprehensive setup instructions including IntelliJ IDEA configuration, troubleshooting, and more, please refer to [SETUP_GUIDE.md](SETUP_GUIDE.md).

## 🗺️ Map Configuration

The map is configured with the following parameters:

- **Center Location**: Colombo, Sri Lanka
- **Latitude**: 6.9271
- **Longitude**: 79.8612
- **Zoom Level**: 12
- **Marker Title**: "Colombo, Sri Lanka"

To change the location, edit the `initMap()` function in `index.html`:

```javascript
const location = { lat: YOUR_LATITUDE, lng: YOUR_LONGITUDE };
```

## 📦 Dependencies

- **jakarta.servlet-api** 5.0.0 (provided)
- **maven-war-plugin** 3.3.2
- **maven-compiler-plugin** 3.11.0

## 🔍 File Descriptions

### pom.xml
Maven project configuration defining dependencies, plugins, and build settings.

### MapServlet.java
Java Servlet that handles HTTP GET requests to the root path (`/`) and forwards them to `index.html`.

### web.xml
Web deployment descriptor that maps the `MapServlet` to the root URL pattern and defines welcome files.

### index.html
HTML page containing:
- A full-viewport `<div>` for the map
- CSS for responsive layout
- JavaScript `initMap()` function to initialize the map
- Google Maps API script tag

## 🛠️ Development

### Build Commands

```bash
# Clean build artifacts
mvn clean

# Compile the project
mvn compile

# Package as WAR
mvn package

# Full clean build
mvn clean package
```

### Running Tests

This is a simple demonstration project without unit tests. For production applications, consider adding:
- JUnit tests for servlet logic
- Integration tests for the web application

## 🐛 Troubleshooting

### Map doesn't load
- Verify your Google Maps API key is valid
- Check that the Maps JavaScript API is enabled in Google Cloud Console
- Open browser Developer Tools (F12) and check for errors

### Build errors
- Ensure JDK 11 or higher is installed
- Verify Maven is properly configured
- Try `mvn clean install -U` to force update dependencies

### Deployment issues
- Check Tomcat logs in `logs/catalina.out`
- Verify port 8080 is not in use
- Ensure you have write permissions to Tomcat directories

## 📄 License

This project is provided as-is for educational and demonstration purposes.

## 👨‍💻 Author

Ushitha Induwara

## 🤝 Contributing

This is a demonstration project. Feel free to fork and modify for your own use.

## 📚 Resources

- [Google Maps JavaScript API Documentation](https://developers.google.com/maps/documentation/javascript)
- [Jakarta Servlet Specification](https://jakarta.ee/specifications/servlet/)
- [Apache Maven Documentation](https://maven.apache.org/guides/)
- [Apache Tomcat Documentation](https://tomcat.apache.org/tomcat-10.0-doc/)
