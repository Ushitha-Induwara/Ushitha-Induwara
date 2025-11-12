# Google Maps Web Application - Setup Guide

This is a simple Java EE web application that displays a Google Map using Maven, Java Servlets, and Apache Tomcat.

## Prerequisites

- **Java Development Kit (JDK)** 11 or higher
- **Apache Maven** 3.6 or higher
- **IntelliJ IDEA** (Community or Ultimate Edition)
- **Apache Tomcat** 9.x or 10.x
- **Google Maps API Key** (Get one from [Google Cloud Console](https://console.cloud.google.com/))

## Project Structure

```
google-maps-webapp/
├── pom.xml
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── example/
│       │           └── map/
│       │               └── MapServlet.java
│       └── webapp/
│           ├── WEB-INF/
│           │   └── web.xml
│           └── index.html
└── README.md
```

## Setup Instructions for IntelliJ IDEA

### Step 1: Open the Project

1. Launch **IntelliJ IDEA**
2. Click **File** → **Open**
3. Navigate to the project directory and select it
4. Click **OK**
5. Wait for IntelliJ to import the Maven project (it should auto-detect `pom.xml`)

### Step 2: Configure Google Maps API Key

1. Open `src/main/webapp/index.html`
2. Find the line with `YOUR_API_KEY_HERE`
3. Replace it with your actual Google Maps API key:
   ```html
   <script async defer
       src="https://maps.googleapis.com/maps/api/js?key=YOUR_ACTUAL_API_KEY&callback=initMap">
   </script>
   ```

### Step 3: Configure Apache Tomcat in IntelliJ IDEA

#### For IntelliJ IDEA Ultimate:

1. Click **Run** → **Edit Configurations**
2. Click the **+** button and select **Tomcat Server** → **Local**
3. In the **Server** tab:
   - Click **Configure** next to the Application server field
   - Navigate to your Tomcat installation directory and select it
   - Click **OK**
4. In the **Deployment** tab:
   - Click the **+** button
   - Select **Artifact** → **google-maps-webapp:war exploded**
   - Set **Application context** to `/` (or `/google-maps-webapp`)
5. Click **Apply** and **OK**

#### For IntelliJ IDEA Community Edition:

IntelliJ Community Edition does not have built-in Tomcat support. You have two options:

**Option A: Use Smart Tomcat Plugin**
1. Go to **File** → **Settings** → **Plugins**
2. Search for "Smart Tomcat" and install it
3. Restart IntelliJ IDEA
4. Click **Run** → **Edit Configurations**
5. Click **+** and select **Smart Tomcat**
6. Configure the Tomcat server path and deployment settings

**Option B: Use Maven and Command Line**
1. Build the WAR file using Maven (see Step 4 below)
2. Deploy manually to Tomcat's `webapps` directory

### Step 4: Build the Project

You can build the project using IntelliJ's Maven tool window or the command line:

#### Using IntelliJ:
1. Open the **Maven** tool window (View → Tool Windows → Maven)
2. Expand **Lifecycle**
3. Double-click **clean** then **package**
4. The WAR file will be created in the `target/` directory

#### Using Command Line:
```bash
mvn clean package
```

The compiled WAR file will be at: `target/google-maps-webapp.war`

### Step 5: Run the Application

#### Using IntelliJ (Ultimate):
1. Click the **Run** button (green triangle) or press **Shift + F10**
2. Wait for Tomcat to start
3. Your default browser should open automatically

#### Using Command Line with Tomcat:
1. Copy the WAR file to Tomcat's webapps directory:
   ```bash
   cp target/google-maps-webapp.war /path/to/tomcat/webapps/
   ```
2. Start Tomcat:
   ```bash
   /path/to/tomcat/bin/startup.sh   # Linux/Mac
   /path/to/tomcat/bin/startup.bat  # Windows
   ```
3. Access the application at: `http://localhost:8080/google-maps-webapp/`

### Step 6: View the Application

Once the server is running, open your web browser and navigate to:
- If context is `/`: `http://localhost:8080/`
- If context is `/google-maps-webapp`: `http://localhost:8080/google-maps-webapp/`

You should see a full-screen Google Map centered on Colombo, Sri Lanka (latitude: 6.9271, longitude: 79.8612) with a marker.

## Troubleshooting

### Map doesn't load / Shows gray screen
- **Check your API key**: Make sure you've replaced `YOUR_API_KEY_HERE` with a valid Google Maps API key
- **Enable required APIs**: In Google Cloud Console, ensure the "Maps JavaScript API" is enabled
- **Check browser console**: Open Developer Tools (F12) and check for JavaScript errors

### Tomcat deployment issues
- **Port conflict**: If port 8080 is already in use, change the Tomcat port in `server.xml` or the run configuration
- **Permission errors**: Make sure you have write permissions to the Tomcat directories
- **Clean and rebuild**: Try `mvn clean package` to rebuild the project

### Maven build errors
- **Java version**: Ensure you're using JDK 11 or higher
- **Maven settings**: Check that Maven is properly configured in IntelliJ (File → Settings → Build, Execution, Deployment → Build Tools → Maven)
- **Dependencies**: Run `mvn clean install` to force download all dependencies

## Technology Stack

- **Backend**: Java Servlet (Jakarta EE)
- **Frontend**: HTML5, CSS3, JavaScript
- **API**: Google Maps JavaScript API
- **Build Tool**: Apache Maven
- **Server**: Apache Tomcat
- **IDE**: IntelliJ IDEA

## Features

- Full-screen responsive Google Map
- Centered on Colombo, Sri Lanka
- Custom marker placement
- Clean, modern UI
- Servlet-based architecture

## Project Files Description

### `pom.xml`
Maven project configuration file that defines:
- Project metadata (groupId, artifactId, version)
- Dependencies (jakarta.servlet-api)
- Build plugins (maven-war-plugin, maven-compiler-plugin)

### `MapServlet.java`
Java Servlet that handles GET requests to the root path (`/`) and forwards to `index.html`

### `web.xml`
Web deployment descriptor that:
- Maps the MapServlet to the URL pattern `/`
- Defines welcome files

### `index.html`
HTML page with:
- Full-viewport map container
- CSS styling for responsive layout
- JavaScript code to initialize Google Maps
- Google Maps API script inclusion

## License

This project is provided as-is for educational purposes.

## Support

For issues or questions, please refer to:
- [Google Maps JavaScript API Documentation](https://developers.google.com/maps/documentation/javascript)
- [Apache Tomcat Documentation](https://tomcat.apache.org/)
- [Maven Documentation](https://maven.apache.org/guides/)
