# Smart Travel Booking System

A comprehensive full-stack travel booking platform with intelligent location autocomplete, real-time data fetching, and complete booking functionality.

## 🚀 Features

### Frontend Features
- **Smart Location Autocomplete**: Debounced search with city, airport, and country suggestions
- **Multi-Service Booking**: Flights, hotels, and travel packages
- **Advanced Search Forms**: Date pickers, traveler count selectors, and filters
- **Real-time Results**: Live data fetching with filtering and sorting
- **Responsive Design**: Mobile-first design that works on all devices
- **User Authentication**: Secure login/register with JWT tokens
- **Booking Management**: User dashboard with booking history

### Backend Features
- **REST API**: Complete API endpoints for all functionality
- **JWT Authentication**: Secure user authentication and authorization
- **Location Search API**: Intelligent autocomplete with external API integration
- **Travel Data APIs**: Mock APIs for flights, hotels, and packages
- **Database Integration**: User and booking data management
- **Error Handling**: Comprehensive error handling and validation

### Key Technical Features
- **Debounced Search**: Optimized API calls with 300ms debounce
- **Smart Suggestions**: Location results with city, airport code, and country
- **Real-time Updates**: Live search results and booking status
- **Secure Transactions**: JWT-based authentication and secure data handling
- **Modular Architecture**: Reusable components and clean code structure

## 🛠️ Technology Stack

### Frontend
- **Next.js 14**: React framework with App Router
- **TypeScript**: Type-safe development
- **Tailwind CSS**: Utility-first CSS framework
- **shadcn/ui**: Modern UI component library
- **React Hooks**: State management and side effects

### Backend
- **Next.js API Routes**: Server-side API endpoints
- **JWT**: JSON Web Tokens for authentication
- **bcryptjs**: Password hashing and security
- **Mock APIs**: Simulated travel data services

### Database Schema
\`\`\`sql
-- Users table
CREATE TABLE users (
  id VARCHAR(255) PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password VARCHAR(255) NOT NULL,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Bookings table
CREATE TABLE bookings (
  id VARCHAR(255) PRIMARY KEY,
  user_id VARCHAR(255) REFERENCES users(id),
  type ENUM('flight', 'hotel', 'package') NOT NULL,
  booking_data JSON NOT NULL,
  total_price DECIMAL(10,2) NOT NULL,
  status ENUM('pending', 'confirmed', 'cancelled') DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Locations table (for autocomplete)
CREATE TABLE locations (
  id VARCHAR(255) PRIMARY KEY,
  name VARCHAR(255) NOT NULL,
  city VARCHAR(255) NOT NULL,
  country VARCHAR(255) NOT NULL,
  code VARCHAR(10),
  type ENUM('city', 'airport') NOT NULL,
  INDEX idx_search (name, city, country, code)
);
\`\`\`

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- npm or yarn

### Installation

1. **Clone the repository**
\`\`\`bash
git clone <repository-url>
cd smart-travel-booking-system
\`\`\`

2. **Install dependencies**
\`\`\`bash
npm install
\`\`\`

3. **Set up environment variables**
Create a `.env.local` file in the root directory:
\`\`\`env
JWT_SECRET=your-super-secret-jwt-key-here
NEXT_PUBLIC_API_URL=http://localhost:3000
\`\`\`

4. **Run the development server**
\`\`\`bash
npm run dev
\`\`\`

5. **Open your browser**
Navigate to [http://localhost:3000](http://localhost:3000)

### Demo Account
Use these credentials to test the application:
- **Email**: demo@smarttravel.com
- **Password**: demo123

## 📁 Project Structure

\`\`\`
smart-travel-booking-system/
├── app/                          # Next.js App Router
│   ├── api/                      # API routes
│   │   ├── auth/                 # Authentication endpoints
│   │   ├── locations/            # Location autocomplete API
│   │   ├── flights/              # Flight search API
│   │   ├── hotels/               # Hotel search API
│   │   └── packages/             # Package search API
│   ├── auth/                     # Authentication pages
│   ├── flights/                  # Flight search results
│   └── page.tsx                  # Home page
├── components/                   # Reusable components
│   ├── ui/                       # shadcn/ui components
│   ├── location-autocomplete.tsx # Smart location search
│   ├── flight-search-form.tsx    # Flight booking form
│   ├── hotel-search-form.tsx     # Hotel booking form
│   ├── package-search-form.tsx   # Package booking form
│   ├── header.tsx                # Navigation header
│   └── footer.tsx                # Site footer
└── lib/                          # Utility functions
\`\`\`

## 🔧 API Endpoints

### Authentication
- `POST /api/auth/register` - User registration
- `POST /api/auth/login` - User login

### Location Search
- `GET /api/locations/search?q={query}` - Location autocomplete

### Travel Search
- `GET /api/flights/search` - Flight search
- `GET /api/hotels/search` - Hotel search  
- `GET /api/packages/search` - Package search

### Booking Management
- `POST /api/bookings` - Create booking
- `GET /api/bookings` - Get user bookings
- `PUT /api/bookings/{id}` - Update booking
- `DELETE /api/bookings/{id}` - Cancel booking

## 🎯 Key Components

### LocationAutocomplete
Smart location search component with:
- Debounced API calls (300ms delay)
- City, airport, and country suggestions
- Keyboard navigation support
- Click-outside to close
- Loading states and error handling

### Search Forms
Comprehensive booking forms with:
- Date range selection
- Passenger/guest count
- Trip type selection (round-trip/one-way)
- Class/room type selection
- Form validation

### Search Results
Advanced results display with:
- Real-time filtering
- Price range sliders
- Airline/hotel filtering
- Sort by price, duration, rating
- Responsive card layouts

## 🔒 Security Features

- **JWT Authentication**: Secure token-based authentication
- **Password Hashing**: bcrypt with salt rounds
- **Input Validation**: Server-side validation for all inputs
- **CORS Protection**: Configured for production security
- **XSS Prevention**: Sanitized user inputs
- **Rate Limiting**: API rate limiting (production ready)

## 🌐 Production Deployment

### Environment Variables
\`\`\`env
JWT_SECRET=your-production-jwt-secret
DATABASE_URL=your-database-connection-string
GOOGLE_PLACES_API_KEY=your-google-places-api-key
AMADEUS_API_KEY=your-amadeus-api-key
BOOKING_COM_API_KEY=your-booking-api-key
\`\`\`

### Build and Deploy
\`\`\`bash
npm run build
npm start
\`\`\`

## 🧪 Testing

### Demo Features
1. **Location Search**: Type "New York" or "London" to see autocomplete
2. **Flight Search**: Search NYC to LAX for sample results
3. **User Authentication**: Use demo account or create new account
4. **Responsive Design**: Test on mobile and desktop

### API Testing
Use tools like Postman or curl to test API endpoints:
\`\`\`bash
# Test location search
curl "http://localhost:3000/api/locations/search?q=new"

# Test flight search
curl "http://localhost:3000/api/flights/search?from=NYC&to=LAX&departureDate=2024-12-01"
\`\`\`

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🆘 Support

For support and questions:
- Create an issue in the repository
- Email: support@smarttravel.com
- Documentation: [docs.smarttravel.com](https://docs.smarttravel.com)

---

**SmartTravel** - Intelligent travel booking made simple 🌍✈️🏨
