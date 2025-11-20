# Agora - AI Philosopher Debate Platform

## Project Specification Document

### 1. Project Overview

**Project Name:** Agora  
**Version:** 1.0 (MVP - Demo)  
**Last Updated:** 2024

**Project Type:** Demo application for presentation session

**Vision Statement:**  
Agora is an interactive platform where users can pose philosophical questions and witness AI-powered philosophers engage in thoughtful, multi-perspective debates. The platform aims to make philosophical discourse accessible, engaging, and educational by leveraging AI to simulate diverse philosophical viewpoints.

**Core Value Proposition:**

- Users submit questions on any topic
- Two AI philosophers with distinct personalities debate the question in real-time
- Real-time streaming debate presentations
- Educational and entertaining exploration of ideas
- Cross-platform support (Web, iOS, Android, Desktop)

---

### 2. User Stories & Use Cases

#### Primary User Stories

##### US-1: Question Submission

- As a user, I want to submit a philosophical question so that I can see different perspectives debated
- Acceptance Criteria:
  - User can enter a question in a text input field
  - Question is validated (length, content appropriateness)
  - User receives confirmation that question is being processed

##### US-2: Debate Viewing

- As a user, I want to watch AI philosophers debate my question so that I can explore different viewpoints
- Acceptance Criteria:
  - Debate displays with clear identification of each philosopher
  - Arguments are presented in a readable, sequential format
  - Each philosopher's response is visually distinct

##### US-3: Philosopher Personalities

- As a user, I want to see philosophers with distinct styles so that debates feel authentic and diverse
- Acceptance Criteria:
  - Each philosopher has a unique name and philosophical tradition
  - Responses reflect their philosophical approach
  - Visual design distinguishes each philosopher

##### US-4: Real-time Streaming

- As a user, I want to see debates stream in real-time so that I can watch the discussion unfold
- Acceptance Criteria:
  - Arguments appear as they are generated
  - Smooth streaming experience without lag
  - Visual indicators show when philosophers are "thinking"

---

### 3. Functional Requirements

#### 3.1 Core Features

##### FR-1: Question Input System

- Text input field for questions (min 10 characters, max 500 characters)
- Question validation (basic length and content checks)
- Simple error handling for invalid inputs
- Users can only submit questions (no interaction during debate for MVP)

##### FR-2: AI Philosopher System

- **2 philosophers per debate** (configurable in settings/config)
- Each philosopher has:
  - Unique name and persona
  - Philosophical tradition/style (e.g., Stoic, Existentialist, Utilitarian, Virtue Ethics)
  - Distinct voice and argumentation style
  - System prompt that defines their approach
- Philosophers take turns presenting arguments
- Each philosopher responds to previous arguments (not just the question)
- Configurable number of participants (default: 2, can be adjusted)

##### FR-3: Real-time Debate Generation

- AI generates debate responses using OpenRouter API (AutoRouter model)
- **Real-time streaming** of responses as they are generated
- Debate format: Sequential turn-based
- Each philosopher's response should:
  - Directly address the question
  - Engage with other philosophers' arguments
  - Maintain character consistency
  - Be substantive (minimum length, avoid generic responses)
- Support for multiple rounds (e.g., opening statements, rebuttals, closing)
- Server-Sent Events (SSE) or WebSocket for streaming

##### FR-4: Debate Display

- **Real-time streaming** of responses as they are generated
- Clear visual distinction between philosophers
- Timestamps for each argument
- Scrollable/expandable debate view
- Cross-platform responsive design (Flutter handles this)
- Loading/thinking indicators during generation
- Auto-scroll to latest argument

##### FR-5: Data Persistence (MVP - Minimal)

- Save debates to PostgreSQL database (for demo purposes)
- No user accounts or authentication (one-off sessions)
- Basic debate storage for potential retrieval during demo
- No search/history features for MVP

#### 3.2 Secondary Features (Out of Scope for MVP)

**Note:** The following features are explicitly out of scope for the MVP demo:

- User accounts and authentication
- Debate history and search
- Social features (sharing, voting, comments)
- Advanced moderation
- User interaction during debates

---

### 4. Technical Requirements

#### 4.1 Architecture

**High-Level Architecture:**

```text
Flutter App (Web/Mobile/Desktop)
    ↓
Serverpod Backend (Dart)
    ↓
OpenRouter API (AutoRouter Model)
    ↓
PostgreSQL Database (Digital Ocean)
```

**Technology Stack (Confirmed):**

**Frontend:**

- **Flutter** - Cross-platform framework (Web, iOS, Android, Desktop)
- Dart language
- State management: Provider, Riverpod, or Bloc
- Real-time updates via Serverpod streaming

**Backend:**

- **Serverpod** - Dart backend framework
- RESTful API endpoints
- Server-Sent Events (SSE) or WebSocket for real-time streaming
- Built-in database ORM

**AI Integration:**

- **OpenRouter API** - AutoRouter model (automatically selects best model)
- Custom system prompts for each philosopher
- Streaming support for real-time responses

**Database:**

- **PostgreSQL** on Digital Ocean
- Schema: Questions, Debates, Arguments, Philosophers
- Serverpod handles database migrations and ORM

**Infrastructure:**

- **Digital Ocean** - Hosting for Serverpod backend and PostgreSQL
- Environment variables for API keys (OpenRouter)
- Basic rate limiting for demo purposes

#### 4.2 Data Models

**Question (Dart/Serverpod Model):**

```dart
class Question {
  int? id;
  String text;
  DateTime createdAt;
  QuestionStatus status; // pending, processing, completed, failed
}
```

**Debate (Dart/Serverpod Model):**

```dart
class Debate {
  int? id;
  int questionId;
  List<int> philosopherIds; // 2 philosophers for MVP
  List<Argument> arguments;
  DebateStatus status; // generating, completed, failed
  DateTime createdAt;
  DateTime? completedAt;
  int rounds;
  int? totalTokens;
}
```

**Argument (Dart/Serverpod Model):**

```dart
class Argument {
  int? id;
  int debateId;
  int philosopherId;
  String philosopherName;
  int round;
  String content;
  DateTime timestamp;
  int order;
}
```

**Philosopher (Dart/Serverpod Model):**

```dart
class Philosopher {
  int id;
  String name;
  String tradition; // e.g., "Stoic", "Existentialist"
  String description;
  String systemPrompt;
  String? avatar; // emoji or icon name
  String color; // hex color for UI
}
```

#### 4.3 Serverpod API Endpoints

**Question Management:**

- `POST /question` - Submit a new question (returns Question)
- `GET /question/:id` - Get question details

**Debate Management:**

- `POST /debate/start` - Start a new debate for a question (returns Debate)
- `GET /debate/:id` - Get debate details
- `GET /debate/:id/stream` - Stream debate generation (SSE/WebSocket)
  - Streams Argument objects as they are generated

**Philosopher Management:**

- `GET /philosopher` - List available philosophers
- `GET /philosopher/:id` - Get philosopher details

**Note:** Serverpod uses code generation for type-safe endpoints. Endpoints will be defined as methods in Serverpod endpoint classes.

---

### 5. User Interface Design

#### 5.1 Key Screens/Components (Flutter)

**Home/Question Input Screen:**

- App title/logo ("Agora")
- Brief description
- Question input form (prominent text field)
- Submit button
- Loading indicator when processing

**Debate View Screen:**

- Question display at top (sticky header)
- Real-time debate timeline/thread view
- Each argument in a card/widget with:
  - Philosopher name and avatar/icon
  - Philosophical tradition badge/chip
  - Argument text (streaming text animation)
  - Timestamp
- Auto-scroll to latest argument
- Loading/thinking indicators when philosophers are generating
- "New Question" button to start over

**Settings/Configuration Screen (Optional for MVP):**

- Number of philosophers selector (default: 2)
- Philosopher selection (if multiple available)

#### 5.2 Design Principles

- **Clarity:** Easy to read, uncluttered interface
- **Distinction:** Clear visual separation between philosophers
- **Accessibility:** WCAG 2.1 AA compliance
- **Responsive:** Works on mobile, tablet, desktop
- **Performance:** Fast loading, smooth interactions

#### 5.3 Color Scheme & Branding

- **Primary Colors:** Consider classical/thoughtful palette (deep blues, warm grays, gold accents)
- **Philosopher Colors:** Each philosopher has a distinct color for easy identification
- **Typography:** Readable serif or sans-serif font for debate text

---

### 6. AI/LLM Integration

#### 6.1 Philosopher System Prompts

Each philosopher needs a detailed system prompt that includes:

- Their philosophical tradition and core beliefs
- Their argumentation style (logical, emotional, practical, etc.)
- How they engage with other viewpoints
- Examples of their typical responses

**Example Philosopher Prompt (Stoic):**

```text
You are Marcus Aurelius, a Stoic philosopher. Your arguments emphasize:
- Virtue as the highest good
- Acceptance of what cannot be controlled
- Logic and reason over emotion
- Practical wisdom and self-discipline
- Engaging respectfully with other viewpoints while maintaining your principles

When debating, you:
- Reference Stoic principles (logos, arete, eudaimonia)
- Use clear, logical reasoning
- Acknowledge valid points from others
- Maintain a calm, measured tone
```

#### 6.2 Debate Generation Strategy (Real-time Streaming)

**Sequential Generation with Streaming:**

1. Generate first philosopher's opening argument (stream tokens to client)
2. Once complete, generate second philosopher's response (including rebuttal, stream tokens)
3. Continue alternating with each philosopher responding to previous arguments
4. Repeat for multiple rounds (e.g., 3-4 rounds)
5. Each argument streams in real-time as tokens are generated

**Implementation Details:**

- Use OpenRouter API streaming endpoint
- Serverpod handles streaming via SSE or WebSocket
- Flutter app receives streamed tokens and updates UI in real-time
- Each philosopher maintains conversation context (all previous arguments)
- Arguments are saved to database as they complete

#### 6.3 Quality Control

- **Length Constraints:** Minimum 100 tokens, maximum 500 tokens per argument
- **Content Filtering:** Ensure arguments are substantive, not generic
- **Consistency Checks:** Verify philosopher maintains character through system prompts
- **Error Handling:** Retry logic (max 2 retries), fallback responses if API fails
- **Streaming Reliability:** Handle connection drops, resume streaming if possible

---

### 7. Non-Functional Requirements

#### 7.1 Performance

- Question submission: < 2 seconds response time
- Debate generation: First argument streams within 5-10 seconds
- Real-time streaming: < 500ms latency between token generation and display
- App load: < 3 seconds
- Support for demo: 5-10 concurrent debates (sufficient for presentation)

#### 7.2 Security

- API key protection (server-side only)
- Input sanitization and validation
- Rate limiting (prevent abuse)
- HTTPS for all communications
- User data privacy (if accounts implemented)

#### 7.3 Scalability

- Database indexing for fast queries
- Caching for frequently accessed debates
- Queue system for debate generation (if high volume)
- CDN for static assets

#### 7.4 Reliability

- Error handling and graceful degradation
- Retry logic for AI API calls
- Monitoring and logging
- Backup and recovery procedures

---

### 8. Development Phases (MVP Focus)

#### Phase 1: Core Setup (Week 1)

- Set up Flutter project structure
- Set up Serverpod backend project
- Configure PostgreSQL database on Digital Ocean
- Set up OpenRouter API integration
- Basic project structure and dependencies

#### Phase 2: Backend Development (Week 1-2)

- Create Serverpod models (Question, Debate, Argument, Philosopher)
- Implement philosopher system prompts (2 philosophers)
- Create debate generation endpoint with OpenRouter streaming
- Implement real-time streaming (SSE/WebSocket)
- Database schema and migrations

#### Phase 3: Frontend Development (Week 2-3)

- Question input screen
- Debate view with real-time streaming
- Philosopher cards/UI components
- State management for streaming updates
- Auto-scroll and loading states
- Cross-platform testing (Web, Mobile)

#### Phase 4: Integration & Polish (Week 3-4)

- Connect frontend to backend
- Test real-time streaming end-to-end
- UI/UX polish and animations
- Error handling and edge cases
- Demo preparation and testing

**Total Timeline:** 3-4 weeks for MVP demo

---

### 9. Success Metrics

#### Key Performance Indicators (KPIs)

- Number of questions submitted per day/week
- Average debate completion rate
- User engagement (time spent viewing debates)
- Return user rate
- Share rate (if sharing implemented)
- User satisfaction (surveys/ratings)

#### Technical Metrics

- API response times
- Error rates
- Uptime percentage
- Cost per debate generation

---

### 10. Risks & Mitigation

#### Technical Risks

- **AI API costs:** High usage could be expensive
  - *Mitigation:* Implement caching, rate limiting, optimize prompts
- **AI response quality:** Debates may be generic or off-character
  - *Mitigation:* Careful prompt engineering, testing, iteration
- **Scalability:** High traffic could overwhelm system
  - *Mitigation:* Queue system, horizontal scaling, caching

#### Product Risks

- **User engagement:** Users may lose interest quickly
  - *Mitigation:* Focus on quality over quantity, iterate based on feedback
- **Content moderation:** Inappropriate questions or AI responses
  - *Mitigation:* Input validation, content filters, moderation tools

---

### 11. Decisions Made

1. **Platform:** ✅ All platforms (Flutter provides cross-platform support)
2. **AI Service:** ✅ OpenRouter with AutoRouter model
3. **Monetization:** ✅ Demo app - not applicable
4. **Philosopher Count:** ✅ 2 participants per debate (configurable)
5. **Debate Format:** ✅ Real-time streaming
6. **User Accounts:** ✅ None for MVP (one-off sessions)
7. **User Interaction:** ✅ Questions only (no interaction during debate)
8. **Tech Stack:** ✅ Flutter/Serverpod/Digital Ocean/PostgreSQL

### 11.1 Remaining Decisions

1. **Debate Length:** How many rounds? (Recommended: 3-4 rounds for demo)
2. **Philosopher Selection:** Which 2 philosophers for initial demo? (See Appendix A)
3. **Philosopher Configuration:** User-selectable or random assignment?
4. **Streaming Method:** SSE or WebSocket? (Serverpod supports both)

---

### 12. Next Steps

1. ✅ **Review this specification** - Completed
2. ✅ **Answer open questions** - Completed
3. ✅ **Choose technology stack** - Flutter/Serverpod/Digital Ocean/PostgreSQL/OpenRouter
4. **Set up development environment:**
   - Initialize Flutter project
   - Initialize Serverpod project
   - Set up Digital Ocean PostgreSQL database
   - Configure OpenRouter API keys
   - Set up project structure
5. **Create initial philosopher prompts** (2 philosophers for MVP)
6. **Develop MVP** following Phase 1-4 plan
7. **Test and prepare for demo presentation**

---

### Appendix A: Example Philosophers

**Suggested Initial Philosopher Roster (Select 2 for MVP):**

1. **Socrates (Socratic Method)**
   - Questions assumptions, seeks definitions
   - "I know that I know nothing"
   - Style: Questioning, dialectical, seeks clarity

2. **Marcus Aurelius (Stoic)**
   - Virtue, acceptance, reason
   - Practical wisdom
   - Style: Calm, logical, emphasizes what we can control

3. **Nietzsche (Existentialist)**
   - Will to power, overcoming, individual creation
   - Provocative, challenging
   - Style: Bold, challenging, emphasizes individual will

4. **Confucius (Virtue Ethics)**
   - Harmony, relationships, moral cultivation
   - Practical ethics
   - Style: Practical, relationship-focused, emphasizes virtue

5. **Simone de Beauvoir (Feminist Existentialist)**
   - Freedom, responsibility, social context
   - Intersectional perspective
   - Style: Thoughtful, considers social implications

6. **John Stuart Mill (Utilitarian)**
   - Greatest good, individual liberty
   - Practical consequences
   - Style: Practical, consequence-focused, emphasizes utility

7. **Immanuel Kant (Deontological)**
   - Categorical imperative, duty, reason
   - Universal principles
   - Style: Rigorous, principle-based, emphasizes duty

**Recommended MVP Pair:** Choose contrasting styles, e.g.:

- **Socrates vs. Marcus Aurelius** (Questioning vs. Stoic acceptance)
- **Nietzsche vs. Kant** (Existentialist vs. Deontological)
- **Mill vs. Kant** (Utilitarian vs. Deontological)

---

**Document Status:** ✅ Complete - Ready for Implementation

---

### Appendix B: OpenRouter Integration Notes

**OpenRouter AutoRouter Model:**

- Automatically selects the best available model
- Supports streaming
- Cost-effective for demo purposes
- API endpoint: `https://openrouter.ai/api/v1/chat/completions`

**Required Configuration:**

- OpenRouter API key (environment variable)
- Streaming enabled: `stream: true`
- Model: `"auto"` or specific model
- System prompts for each philosopher
- Temperature: 0.7-0.9 for creative but consistent responses

**Streaming Implementation:**

- Use Server-Sent Events (SSE) or WebSocket
- Parse streaming JSON responses
- Update Flutter UI in real-time as tokens arrive
