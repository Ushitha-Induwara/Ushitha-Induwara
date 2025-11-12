# Google Maps Web Application Setup Guide

## Overview
This is a simple Java EE web application that displays a Google Map centered on Colombo, Sri Lanka. The application is built with Maven and runs on Apache Tomcat.

## Prerequisites
- **Java Development Kit (JDK) 11 or higher**
- **Apache Maven** (for building the project)
- **IntelliJ IDEA** (Ultimate Edition recommended for built-in Tomcat support)
- **Apache Tomcat 10** (compatible with Jakarta EE 9+)
- **Google Maps API Key** (obtain from [Google Cloud Console](https://console.cloud.google.com/))

## Project Structure
```
google-map-app/
├── pom.xml
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── map/
│       │               └── MapServlet.java
│       └── webapp/
│           ├── index.html
│           └── WEB-INF/
│               └── web.xml
└── README_SETUP.md
```

## Setup Instructions for IntelliJ IDEA

### Step 1: Open the Project
1. Launch **IntelliJ IDEA**
2. Select **File → Open**
3. Navigate to the project directory and select the `pom.xml` file
4. Click **Open as Project**
5. IntelliJ will automatically import the Maven dependencies

### Step 2: Configure Tomcat Server
1. Go to **Run → Edit Configurations**
2. Click the **+** button and select **Tomcat Server → Local**
3. If Tomcat is not configured:
   - Click **Configure** next to the Application Server field
   - Click **+** and browse to your Tomcat installation directory
   - Click **OK**
4. In the **Deployment** tab:
   - Click **+** → **Artifact**
   - Select **google-map-app:war exploded**
   - Set **Application context** to `/` (root context)
5. Click **Apply** and **OK**

### Step 3: Add Your Google Maps API Key
1. Open `src/main/webapp/index.html`
2. Find the line containing `YOUR_API_KEY_HERE`
3. Replace it with your actual Google Maps API key:
   ```html
   <script src="https://maps.googleapis.com/maps/api/js?key=YOUR_ACTUAL_API_KEY&callback=initMap" async defer></script>
   ```

### Step 4: Build the Project
Using Maven command line:
```bash
mvn clean package
```

Or using IntelliJ:
1. Open the **Maven** tool window (View → Tool Windows → Maven)
2. Expand **Lifecycle**
3. Double-click **clean** then **package**

### Step 5: Run the Application
1. Click the **Run** button (green triangle) or press **Shift + F10**
2. IntelliJ will start Tomcat and deploy the application
3. Your default browser should open automatically to `http://localhost:8080/`
4. You should see a Google Map centered on Colombo, Sri Lanka with a marker

## Troubleshooting

### Map doesn't display
- **Check API Key**: Ensure you've replaced `YOUR_API_KEY_HERE` with a valid Google Maps API key
- **Enable APIs**: Make sure the Maps JavaScript API is enabled in your Google Cloud Console
- **Check Browser Console**: Open browser developer tools (F12) to see any JavaScript errors

### Tomcat fails to start
- **Port Conflict**: Ensure port 8080 is not in use by another application
- **Tomcat Version**: Use Tomcat 10.x or higher for Jakarta EE compatibility

### Build errors
- **Java Version**: Verify you're using JDK 11 or higher
- **Maven Settings**: Run `mvn clean install -U` to force update dependencies

## Alternative: Running with Maven Tomcat Plugin
If you prefer using Maven instead of IntelliJ's Tomcat integration, you can add the following plugin to `pom.xml`:

```xml
<plugin>
    <groupId>org.apache.tomcat.maven</groupId>
    <artifactId>tomcat7-maven-plugin</artifactId>
    <version>2.2</version>
    <configuration>
        <path>/</path>
        <port>8080</port>
    </configuration>
</plugin>
```

Then run:
```bash
mvn tomcat7:run
```

## Features
- **Full-screen Google Map**: The map occupies the entire viewport
- **Centered on Colombo**: Coordinates (6.9271, 79.8612)
- **Marker**: A single marker placed at the center location
- **Responsive**: The map adapts to different screen sizes

## Technology Stack
- **Backend**: Java Servlet (Jakarta Servlet API 5.0)
- **Frontend**: HTML5, CSS3, JavaScript
- **API**: Google Maps JavaScript API
- **Build Tool**: Apache Maven
- **Server**: Apache Tomcat 10.x

## Customization
To change the map location, edit `src/main/webapp/index.html`:
```javascript
// Change these coordinates
const colombo = { lat: 6.9271, lng: 79.8612 };
```

To adjust the zoom level:
```javascript
const map = new google.maps.Map(document.getElementById("map"), {
    zoom: 12,  // Change this value (1-20)
    center: colombo,
    mapTypeId: 'roadmap'
});
```

## License
This is a simple example application for educational purposes.
