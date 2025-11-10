# EduInsight Engine

Engineering College Performance Analytics Platform

## Overview

EduInsight Engine is a comprehensive web platform designed to transform raw academic data into actionable insights for engineering college stakeholders. It provides dynamic, real-time analytics to reduce time-to-insight for student performance analysis by 70%, enable data-driven curriculum decisions, and offer immediate access to academic standing and progression trends.

## Features

### For Educators
- **Targeted Dashboards**: Reduce time-to-insight for student performance analysis
- **Section Management**: Quick access to assigned sections and student alerts
- **Performance Correlation**: Attendance and academic performance analytics

### For Administrators
- **College-wide KPIs**: Pass percentages, average CGPA, total students metrics
- **Branch Comparisons**: Interactive bar charts comparing CSE, ECE, ME, CE performance
- **Trend Analysis**: Semester-over-semester performance tracking

### For Students
- **Personal Analytics**: CGPA progression line charts and section ranking
- **Academic Standing**: Immediate access to performance indicators
- **Progression Trends**: Semester-wise performance breakdown

## Technical Architecture

### Frontend Stack
- **Framework**: React.js with TypeScript
- **UI Library**: Material-UI (MUI) v5
- **State Management**: Redux Toolkit
- **Routing**: React Router v6
- **Charts**: Chart.js with react-chartjs-2
- **Hosting**: Vercel

### Backend Stack
- **Framework**: Node.js with Express.js & TypeScript
- **Database**: PostgreSQL with Prisma ORM
- **Authentication**: JWT tokens with role-based access
- **File Processing**: Multer for Excel data imports
- **Hosting**: Heroku or Railway

## Database Schema

### Users Table
```sql
id | email | password_hash | role ('admin', 'faculty', 'student') | created_at | updated_at
```

### Students Table
```sql
id | roll_number | name | branch | section | email | semester_1_sgpa | semester_2_sgpa | cgpa | created_at | updated_at
```

### Faculty Assignments Table
```sql
id | faculty_id | branch | section | academic_year
```

### Academic Sessions Table
```sql
id | student_id | semester | sgpa | credits_completed | academic_year | created_at
```

## Security & Access Control

### Authentication Flow
- JWT token with 24-hour expiration
- Role-based route protection
- Password hashing with bcrypt

### Access Matrix
- **Admin**: Full access to all features
- **Faculty**: Dashboard, analytics for assigned sections, student profiles (their students only)
- **Student**: Personal dashboard, profile, performance data only

## Installation & Setup

### Prerequisites
- Node.js (v16 or higher)
- PostgreSQL database
- npm or yarn package manager

### Backend Setup

1. Navigate to the backend directory:
```bash
cd backend
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
Create a `.env` file with:
```env
DATABASE_URL="postgresql://username:password@localhost:5432/eduinsight"
JWT_SECRET="your-secret-key"
PORT=5000
```

4. Run database migrations:
```bash
npx prisma migrate dev
```

5. Generate Prisma client:
```bash
npx prisma generate
```

6. Start the development server:
```bash
npm run dev
```

### Frontend Setup

1. Navigate to the frontend directory:
```bash
cd frontend
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
Create a `.env` file with:
```env
REACT_APP_API_URL=http://localhost:5000/api
```

4. Start the development server:
```bash
npm start
```

## Data Import

The platform supports Excel file uploads for bulk student data import. Required columns:
- `roll_number`
- `name`
- `branch`
- `section`
- `semester_1_sgpa`
- `semester_2_sgpa`
- `cgpa`

## Analytics Calculations

### Pass Percentage
```
(Students with CGPA ≥ 5.0 / Total Students) × 100
```

### Performance Distribution
Count students in CGPA ranges:
- 9+: Excellent
- 8-9: Very Good
- 7-8: Good
- 6-7: Satisfactory
- Below 6: Needs Improvement

### Trend Analysis
Semester-over-semester performance deltas and ranking calculations.

## API Endpoints

### Authentication
- `POST /api/auth/login` - User login
- `POST /api/auth/register` - User registration (admin only)

### Students
- `GET /api/students` - Get all students (admin/faculty)
- `GET /api/students/:id` - Get student details
- `POST /api/students` - Create student record
- `PUT /api/students/:id` - Update student record
- `DELETE /api/students/:id` - Delete student record

### Analytics
- `GET /api/analytics/overview` - College-wide KPIs
- `GET /api/analytics/branch/:branch` - Branch-specific analytics
- `GET /api/analytics/section/:section` - Section-specific analytics

### Import
- `POST /api/import/students` - Upload Excel file for student data

## Development Phases

### Phase 1: Foundation (Current)
- ✅ PostgreSQL database setup with schema
- ✅ Express.js backend with basic CRUD operations
- ✅ React frontend with routing structure
- ✅ Basic authentication system

### Phase 2: Data Pipeline
- Excel parser for student data
- Database seeding script
- Data validation middleware
- Bulk import interface

### Phase 3: Core Features
- Role-based dashboards
- Student profile pages
- Basic analytics calculations
- Chart integrations

### Phase 4: Advanced Analytics
- Comparative analysis tools
- Performance trend visualizations
- Export functionality (PDF, CSV)

### Phase 5: Polish & Deployment
- Responsive design testing
- Security audit
- Performance optimization
- Production deployment

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, email support@eduinsight.com or join our Slack channel.

## Roadmap

- [ ] Mobile application development
- [ ] Integration with learning management systems
- [ ] Advanced predictive analytics using machine learning
- [ ] Real-time notifications and alerts
- [ ] Multi-language support
