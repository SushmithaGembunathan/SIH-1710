# Smart India Hackathon Workshop
# Date: 16-10-2026
## Register Number: 212224040342
## Name:Sushmitha Gembunathan
## Problem Title
SIH 1710: Enhancing Navigation for Railway Station Facilities and Locations
## Problem Description
Background: Railway stations are complex environments with numerous facilities and locations such as ticket counters, platforms, restrooms, food courts, and waiting areas. Passengers often face difficulties in navigating these spaces, especially in large or unfamiliar stations. Efficient and user-friendly navigation systems are crucial for improving passenger experience, reducing congestion, and ensuring timely travel connections. Description: The problem involves developing a comprehensive navigation solution for railway stations that assists passengers in locating various facilities and destinations within the station premises. This includes creating detailed maps, providing real-time directions, and integrating features such as accessibility options for individuals with disabilities. The solution should be intuitive, easy to use, and accessible via multiple platforms, including mobile devices and digital kiosks. Key challenges include updating navigation information in real-time, ensuring accuracy, and accommodating the diverse needs of all passengers. Expected Solution: The expected solution is a multi-platform navigation system that provides detailed, real-time directions to all facilities and locations within a railway station. This system should include: A mobile application with 3D interactive maps and step-by-step navigation. Digital kiosks located throughout the station with touch-screen interfaces. Voice-guided navigation for visually impaired passengers. Regular updates to reflect changes in station layout and facility locations. Integration with existing railway apps and services for seamless user experience. The solution should enhance the overall passenger experience by reducing confusion, saving time, and improving accessibility within the station.

## Problem Creater's Organization
Ministry of Railway

## Idea

Large railway stations confuse passengers: finding the right platform, ticket counter, restroom, food court or waiting hall is slow, especially for first-time travellers, senior citizens, and persons with disabilities.
RGuide is a multi-platform indoor navigation system that gives real-time, step-by-step, accessible directions to every facility inside a station.

### Unique Selling Point : 
. 3D interactive map : 
      Floor-wise 3D station model with route overlay (React + Three.js)
      
. Accessible routing:
      Step-free, lift-only, wide-path routes for wheelchair/elderly users
      
. Voice-guided navigation:
      Turn-by-turn spoken instructions for visually impaired users (multi-language)
      
. Kiosk mode:
      Touch-screen kiosks with "You are here" QR handoff to the phone
      
. Real-time updates:
      Admin changes (platform change, lift down, closed gate) reach all users instantly via WebSockets
      
.Train-aware:
    Enter PNR / train number → auto-navigate to the correct platform and coach position
    
.Works offline:
    PWA caches station map and routing graph; QR-based positioning when GPS/BLE is unavailable
    
.Integration:
    Pluggable adapters for IRCTC / NTES / UTS / RailMadad APIs

## Proposed Solution / Architecture Diagram

### Approach : 
1) Digitise the station – floor plans converted to a navigable graph (nodes = junctions/POIs, edges = walkways, stairs, lifts, escalators, ramps).
2) Locate the user – hybrid indoor positioning: QR codes at landmarks (zero-cost, works everywhere) + BLE beacons (optional) + Wi-Fi/GPS for outdoor approach.
3) Compute the route – A* search on the graph with weighted edges per user profile (fastest, least-crowded, step-free, shortest walk).
4) Guide the user – 3D map, text steps, and voice prompts; auto-reroute if the user deviates or a path is blocked.
5) Keep data fresh – Admin dashboard updates the graph; changes are broadcast via WebSockets and cached in Redis.
   
<img width="1890" height="1185" alt="image" src="https://github.com/user-attachments/assets/421da54e-1c99-4987-ab47-4aec8956a8af" />



## 3. Use Cases

- **First-time passenger:** searches "Platform 5" or "Restroom" and gets a 3D route with step-by-step directions.
- **Visually impaired passenger:** turns on voice mode and hears turn-by-turn spoken guidance.
- **Wheelchair user or senior citizen:** picks "Step-free" and gets routes using only ramps and working lifts.
- **Ticketed traveller:** enters a PNR or train number and is guided to the correct platform and coach position.
- **Kiosk user:** chooses a destination on the touchscreen and scans a QR code to continue on their phone.
- **Station admin or staff:** marks a gate closed or changes a platform, and every active user's route updates instantly.
- **Emergency:** one tap shows the nearest exit, medical room, help desk or RPF post.
- **Regional-language user:** switches the app and voice to Hindi, Tamil, Telugu, Bengali or English.
- **Crowd management:** a crowd heatmap helps suggest less-crowded alternate routes.



## Technology Stack
- **React 18 +:**  Vite	Builds the passenger app, kiosk UI and admin dashboard from one codebase
- **Tailwind CSS:**	Quick responsive styling, with large-text and high-contrast modes
- **Three.js +:** React Three Fiber	The 3D interactive station map and route overlay
- **Zustand	App state:** current location, destination and route
- **Web Speech API:**	Voice search and spoken turn-by-turn directions
- **html5-qrcode / Web Bluetooth:**	Indoor positioning through QR codes and BLE beacons
- **Node.js +:** Express	REST APIs for routes, facilities and alerts
- **Astar algorithm:**	Finds the best path, with accessibility-based edge weights
- **Socket.IO:**	Live updates such as lift down, platform change and reroute
- **PostgreSQL + PostGIS:**	Stores the station map, POIs and walkway graph
- **Redis	Caches:** routes and handles Pub/Sub for real-time events
- **JWT + bcrypt:**	Secure admin and staff login with role-based access
- **NTES / IRCTC APIs:**	Live train status and platform numbers
- **Docker + GitHub Actions:**	Easy deployment and automated builds

## Dependencies

**Frontend:** `react`, `react-dom`, `react-router-dom`, `zustand`, `axios`, `socket.io-client`, `three`, `@react-three/fiber`, `@react-three/drei`, `i18next`, `html5-qrcode`, `tailwindcss`, `vite`, `vite-plugin-pwa`

**Backend:** `express`, `cors`, `socket.io`, `pg`, `ioredis`, `jsonwebtoken`, `bcryptjs`, `dotenv`, `zod`

**Requirements:** Node.js 18+, PostgreSQL with PostGIS, Redis
