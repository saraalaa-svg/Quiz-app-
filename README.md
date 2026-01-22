# Quiz-app-
Testing
import React, { useState, useEffect } from 'react';
import { CheckCircle, XCircle, ChevronRight, Menu, BookOpen, RefreshCw, Star, Bookmark, AlertCircle } from 'lucide-react';

const QuizApp = () => {
  const [activeSection, setActiveSection] = useState(0);
  const [answers, setAnswers] = useState({});
  const [sidebarOpen, setSidebarOpen] = useState(true);
  // New States for Bookmarks and Review Mode
  const [bookmarks, setBookmarks] = useState([]);
  const [viewMode, setViewMode] = useState('normal'); // 'normal', 'bookmarks', 'mistakes'

  // Data extracted from the provided text
  const sections = [
    {
      title: "1. Group 7 (Network integration)",
      questions: [
        // Page 1 - T/F
        { id: "p1-tf1", type: "tf", q: "Physician-hospital alignment in CI requires trust and transparency.", a: "True" },
        { id: "p1-tf2", type: "tf", q: "The CI program allows physicians to participate in care redesign and protocol development", a: "True" },
        { id: "p1-tf3", type: "tf", q: "Performance improvement initiatives do not require data to monitor performance", a: "False" },
        { id: "p1-tf4", type: "tf", q: "Hiring an in-house network engineering team is usually cheaper than using network integration services", a: "False" },
        { id: "p1-tf5", type: "tf", q: "Nurses help in the formation and maintenance of electronic health records", a: "True" },
        { id: "p1-tf6", type: "tf", q: "Participation criteria help ensure doctors follow program requirements", a: "True" },
        { id: "p1-tf7", type: "tf", q: "Good network design and integration services help reduce disruptions caused by network issues", a: "True" },
        { id: "p1-tf8", type: "tf", q: "Health information exchanges are becoming more popular and can support clinically integrated initiatives", a: "True" },
        { id: "p1-tf9", type: "tf", q: "Networking integrators are specialists with expertise in areas such as security, wiring and hardware, connectivity, and administration", a: "True" },
        { id: "p1-tf10", type: "tf", q: "The distribution methodology should be transparent and easy to understand", a: "True" },
        // Page 1 - MCQ
        { id: "p1-mcq1", type: "mcq", q: "Clinical Integration legally can be created within:", options: ["Physician-hospital organization", "Pharmacy chain", "Insurance company", "Government agency"], a: 0 },
        // Page 2 - MCQ
        { id: "p2-mcq1", type: "mcq", q: "A vital step to achieve physician leadership is:", options: ["Reducing communication", "Strong communication strategy across the network", "Eliminating physicians from planning", "Ignoring clear goals"], a: 1 },
        { id: "p2-mcq2", type: "mcq", q: "One advantage of using an outsourced network design and integration service:", options: ["It increases the stress on the IT budget", "It provides improved performance", "It requires training an in-house team", "It uses limited resources of the organization"], a: 1 },
        { id: "p2-tf3", type: "tf", q: "\"One network design works for all organizations and does not need customization.\"", a: "False" },
        { id: "p2-mcq4", type: "mcq", q: "Businesses often face losses due to:", options: ["Marketing problems", "IT errors", "Employee absence", "Customer complaints"], a: 1 },
        { id: "p2-mcq5", type: "mcq", q: "One of the biggest benefits of hiring network integration services is:", options: ["Increased workload", "Reduced cost", "Higher risk", "Less efficiency"], a: 1 },
        { id: "p2-mcq6", type: "mcq", q: "The main goal of performance improvement initiatives is to:", options: ["Increase waste", "Improve quality and reduce variation", "Increase costs", "Eliminate physician involvement"], a: 1 },
        { id: "p2-mcq7", type: "mcq", q: "One factor in selecting performance improvement initiatives is:", options: ["Number of hospital beds", "Low number of staff", "Improvement opportunity", "Patient age"], a: 2 },
        // Page 3
        { id: "p3-mcq1", type: "mcq", q: "Which of the following is a major barrier to integration?", options: ["Clear roles and responsibilities", "Lack of strategic alignment", "Good communication", "Strong leadership"], a: 1 },
        { id: "p3-mcq2", type: "mcq", q: "One role of the nurse is to:", options: ["Ignore data quality", "Destroy electronic records", "Identify data elements for interfaces", "Avoid system involvement"], a: 2 },
        { id: "p3-mcq3", type: "mcq", q: "Business continuity services help businesses mainly by:", options: ["Increasing the number of customers", "Restoring operations after disasters", "Reducing employee workload", "Designing company logos"], a: 1 },
        { id: "p3-mcq4", type: "mcq", q: "Enhanced network security can be achieved by:", options: ["Ignoring IT threats", "Using outdated technology", "Getting services from a skilled network design and integration company", "Reducing the size of the IT team"], a: 2 },
        { id: "p3-mcq5", type: "mcq", q: "What must member physicians sign to join the CI network?", options: ["Work schedule", "Participation agreement", "Patient report", "Medical license"], a: 1 },
        { id: "p3-mcq6", type: "mcq", q: "One example of participation criteria is:", options: ["Ignoring clinical protocols", "Maintaining appropriate IT infrastructure", "Avoiding contracts", "Closing the CI website"], a: 1 },
        { id: "p3-mcq7", type: "mcq", q: "What is the main purpose of Information Technology (IT) in healthcare?", options: ["Making hospitals bigger", "Improving coordination and connectivity between care providers", "Training nurses only", "Reducing doctor numbers"], a: 1 },
        // Page 4
        { id: "p4-mcq1", type: "mcq", q: "A patient registry is mainly used to:", options: ["Store hospital bills", "Track clinical information for specific diseases", "Record doctors' schedules", "Track hospital meals"], a: 1 },
        { id: "p4-mcq2", type: "mcq", q: "Clinical Integration is commonly defined as:", options: ["A system where hospitals compete to increase profits", "A health network working together using proven protocols and measures to improve patient care", "A method of separating hardware components into individual networks", "A process that focuses only on reducing staff workload"], a: 1 },
        { id: "p4-mcq3", type: "mcq", q: "Networking integration mainly involves:", options: ["Adding extra staff to manage patient flow", "Combining different hardware and software components into an integrated network system", "Removing software components to simplify administration", "Disconnecting systems to reduce security risks"], a: 1 },
        { id: "p4-mcq4", type: "mcq", q: "CI incentives are distributed after:", options: ["A meeting", "Performance is achieved", "Signing contracts", "Opening a website"], a: 1 },
        { id: "p4-mcq5", type: "mcq", q: "Funds in CI networks are usually distributed based on:", options: ["Random choice", "Personal friendships", "Measurable performance", "Age of physicians"], a: 2 },
      ]
    },
    {
      title: "2. Electronic Patient Record (EPR)",
      questions: [
        // Page 5
        { id: "p5-mcq1", type: "mcq", q: "The Electronic Patient Record (EPR) is commonly referred to by which of the following alternative names?", options: ["Medical report", "Patient chart", "Health record", "All of the above"], a: 3 },
        { id: "p5-mcq2", type: "mcq", q: "The single overarching goal of the many uses of a patient record is to further the application of health sciences in ways that improve:", options: ["Administrative tasks and billing speed", "The well-being of patients, including research and public health activities", "The availability of printed paper copies", "The number of students receiving instruction"], a: 1 },
        { id: "p5-mcq3", type: "mcq", q: "What are the three primary types of medical records mentioned in the content:", options: ["Physical record, Virtual record, Mixed record", "Paper-based record, Hybrid record, Electronic Medical Record (EMR)", "Patient record, Clinical record, Administrative record", "Digital record, Physical chart, Comprehensive record"], a: 1 },
        { id: "p5-mcq4", type: "mcq", q: "A major advantage of the paper-based medical record is that it is:", options: ["Available 100% of the time and easily accessible", "Organized consistently by problem list", "Simple, requires no formal training, and has no initial high cost", "Easy to share simultaneously with multiple users"], a: 2 },
        { id: "p5-mcq5", type: "mcq", q: "Which of the following is a significant drawback of the Paper-Based record related to Content Quality?", options: ["The format is fragmented and organized chronologically", "Simultaneous use by multiple users is impossible", "Data may be missing, lost, illegible, or incomplete", "It lacks the ability to monitor performance"], a: 2 },
        { id: "p5-mcq6", type: "mcq", q: "Which statement accurately describes a Hybrid Medical Record?", options: ["A record that has been fully converted from paper to electronic format", "A record consisting of both paper documents and electronic documents, often housed in separate locations", "An electronic-only record accessed via two different network systems", "A paper record that is manually updated using a computer"], a: 1 },
        { id: "p5-mcq7", type: "mcq", q: "A key disadvantage of the Hybrid Medical Record is related to cost and staffing, specifically:", options: ["The huge initial conversion cost to electronic format", "It eliminates the need for any paper-handling staff", "It requires extra staff to maintain both the manual and electronic record systems", "It avoids downtime completely, increasing initial labor costs"], a: 2 },
        { id: "p5-mcq8", type: "mcq", q: "Which of the following is an alternative term for the Electronic Health Record (EHR) mentioned in the document:", options: ["Traditional Patient Record (TPR)", "Manual Clinical Management Report (CMR)", "Office Training Log (OTL)", "Computer-based Clinical Information System (ECIS)"], a: 3 },
        // Page 6
        { id: "p6-mcq1", type: "mcq", q: "Which of the following is an example of a Productivity and Financial Improvement benefit of using an EMR?", options: ["Easier management of chronic diseases", "Reduced prescription errors", "Improved coding of visits and enhanced reimbursement", "Rapid access to patient information remotely"], a: 2 },
        { id: "p6-mcq2", type: "mcq", q: "Which benefit of the EMR falls under Improving Quality of Care?", options: ["Less \"chart chasing\"", "More efficient patient billing", "Integrating clinical guidelines and supporting clinical decision-making", "Reduced transcription costs"], a: 2 },
        // Part 2 T/F
        { id: "p6-tf1", type: "tf", q: "The EMR typically represents the medical record within a large, interconnected regional healthcare system.", a: "False" },
        { id: "p6-tf2", type: "tf", q: "The EMR is generally considered less flexible and harder to expand compared to the paper-based record.", a: "False" },
        { id: "p6-tf3", type: "tf", q: "The EHR received its first major endorsement in the year 2001, according to the IOM report.", a: "False" },
        { id: "p6-tf4", type: "tf", q: "The manager's role in EMR implementation is solely focused on handling system maintenance and hardware issues.", a: "False" },
        { id: "p6-tf5", type: "tf", q: "The primary challenge for EHR implementation in Egyptian hospitals is staff resistance to change and new systems.", a: "True" },
        { id: "p6-tf6", type: "tf", q: "A major advantage of the paper-based record is that it allows for simultaneous access by multiple authorized users.", a: "False" },
        { id: "p6-tf7", type: "tf", q: "IOM characteristics require the EMR to support confidentiality, privacy, and continuous audit trails.", a: "True" },
        { id: "p6-tf8", type: "tf", q: "The Hybrid Medical Record consists only of electronic documents.", a: "False" },
        { id: "p6-tf9", type: "tf", q: "One of the EMR benefits for job satisfaction is the reduction in the time spent \"chart chasing\".", a: "True" },
        { id: "p6-tf10", type: "tf", q: "According to IOM, the EMR should allow access to users only during specific scheduled office hours.", a: "False" }
      ]
    },
    {
      title: "3. Artificial intelligence (Pdf)",
      questions: [
        // Page 7
        { id: "p7-mcq1", type: "mcq", q: "ARTIFICIAL INTELLIGENCE REFERS TO:", options: ["Human biology", "Simulation of human intelligence in machines", "Mechanical automation", "Social interaction"], a: 1 },
        { id: "p7-tf2", type: "tf", q: "Weak AI systems are designed to perform one specific task.", a: "True" },
        { id: "p7-mcq3", type: "mcq", q: "Which of the following is an example of strong AI?", options: ["Amazon's Alexa", "Self-driving cars", "Chess game", "Siri"], a: 1 },
        { id: "p7-tf4", type: "tf", q: "AI can definitely assist physicians and nurses.", a: "True" },
        { id: "p7-mcq5", type: "mcq", q: "The main purpose of using AI in managing medical records is to:", options: ["Replace doctors", "Provide faster and more consistent data access", "Create new diseases", "Stop digital automation"], a: 1 },
        { id: "p7-mcq6", type: "mcq", q: "IN RADIOLOGY, AI HELPS TO:", options: ["Increase manual work", "Analyze X-rays and scans faster and more accurately", "Replace CT machines", "Reduce medical data"], a: 1 },
        { id: "p7-tf7", type: "tf", q: "AI in drug creation reduces both time and cost in pharmaceutical trials.", a: "True" },
        { id: "p7-mcq8", type: "mcq", q: "Digital consultation apps like Babylon:", options: ["Offer medical advice using AI", "Only collect blood samples", "Replace nurses", "Work without internet"], a: 0 },
        // Page 8
        { id: "p8-tf1", type: "tf", q: "The role of nurses will completely disappear due to AI.", a: "False" },
        { id: "p8-mcq2", type: "mcq", q: "“Molly” developed by Sense.ly is a:", options: ["Robotic surgeon", "Digital nurse for patient follow-up", "Medical textbook", "Health insurance system"], a: 1 },
        { id: "p8-tf3", type: "tf", q: "AI IN PRECISION MEDICINE USES GENETIC DATA TO PREDICT FUTURE DISEASES.", a: "True" },
        { id: "p8-mcq4", type: "mcq", q: "The AiCure app was created to:", options: ["Confirm medication adherence using a smartphone camera", "Diagnose new diseases", "Replace pharmacists", "Conduct surgeries"], a: 0 },
        { id: "p8-tf5", type: "tf", q: "One of the benefits of AI in healthcare is reducing diagnostic and therapeutic errors.", a: "True" },
        { id: "p8-mcq6", type: "mcq", q: "Wearable health trackers like FitBit can:", options: ["Monitor heart rate and activity level", "Perform medical operations", "Replace physicians", "Prescribe medication"], a: 0 },
        { id: "p8-tf7", type: "tf", q: "AI helps make real-time health risk alerts and predictions.", a: "True" },
        // Page 9
        { id: "p9-mcq1", type: "mcq", q: "“SOPHIA” IS A ROBOT DESIGNED TO:", options: ["Work as a hospital manager", "Serve as a social companion for elderly people", "Replace doctors", "Do repetitive nursing tasks"], a: 1 },
        { id: "p9-tf2", type: "tf", q: "Data privacy and security are not considered challenges in AI healthcare systems.", a: "False" },
        { id: "p9-mcq3", type: "mcq", q: "Robotic surgical systems help surgeons to perform operations with:", options: ["Less accuracy", "Greater accuracy", "More pain", "Larger incisions"], a: 1 },
        { id: "p9-tf4", type: "tf", q: "Incentives for sharing medical data help improve AI systems.", a: "True" },
        { id: "p9-mcq5", type: "mcq", q: "One advantage of robotic surgery is:", options: ["Increased bleeding", "Slower recovery", "Smaller incisions", "More complications"], a: 2 },
      ]
    },
    {
      title: "4. Smart Hospital",
      questions: [
        // Page 10 - MCQs with Key (P12)
        { id: "p10-mcq1", type: "mcq", q: "Smart hospitals mainly rely on:", options: ["Traditional medical tools", "ICT and IoT technologies", "Manual patient records", "Non-digital communication systems"], a: 1 },
        { id: "p10-mcq2", type: "mcq", q: "Which of the following is one of the benefits of smart hospitals?", options: ["Increased greenhouse gas emissions", "Higher electricity bills", "Improved air quality", "Less access to healthcare"], a: 2 },
        { id: "p10-mcq3", type: "mcq", q: "One of the disadvantages of medical technology is:", options: ["Faster recovery", "Increased cost of treatment", "Better accuracy", "Better communication"], a: 1 },
        { id: "p10-mcq4", type: "mcq", q: "Data security in smart hospitals requires:", options: ["Avoiding cybersecurity measures", "Ignoring privacy regulations", "Storing data manually", "Implementing strong cybersecurity & following regulations like HIPAA"], a: 3 },
        { id: "p10-mcq5", type: "mcq", q: "Smart hospitals improve patient experience using technologies such as:", options: ["Manual appointment booking", "Paper-based records", "Virtual consultations & mobile health apps", "Reducing patient-doctor interaction"], a: 2 },
        { id: "p10-mcq6", type: "mcq", q: "Which of the following is a major challenge for smart hospitals?", options: ["Increasing noise", "Reducing network strength", "Improving communication between staff and patients", "Removing wireless systems"], a: 2 },
        { id: "p10-mcq7", type: "mcq", q: "The Internet of Medical Things (loMT) helps in:", options: ["Disconnecting medical devices", "Increasing energy consumption", "Improving operational efficiency & sustainability", "Removing digital systems"], a: 2 },
        { id: "p10-mcq8", type: "mcq", q: "An important recommendation for building a smart hospital is:", options: ["Reducing cybersecurity", "Avoiding IT governance", "Conducting risk and vulnerability assessments", "Stopping IoT investments"], a: 2 },
        { id: "p10-mcq9", type: "mcq", q: "In future smart hospitals, clinicians will use:", options: ["Multiple communication devices", "One integrated device for communication and alerts", "Only paper-based charts", "No digital tools"], a: 1 },
        // Page 11
        { id: "p11-mcq10", type: "mcq", q: "Smart patient rooms will allow patients to:", options: ["Only speak with nurses physically", "Avoid interacting with family", "Control room settings and communicate via bedside consoles", "Block video consultations"], a: 2 },
        { id: "p11-mcq11", type: "mcq", q: "Which technology is primarily used in smart hospitals to monitor patient health remotely?", options: ["Virtual Reality (VR)", "Internet of Things (IoT)", "Blockchain", "3D Printing"], a: 1 },
        { id: "p11-mcq12", type: "mcq", q: "What is one of the main benefits of using AI in smart hospitals?", options: ["Increasing staff numbers", "Improving diagnosis accuracy", "Reducing internet usage", "Eliminating medical imaging"], a: 1 },
        { id: "p11-mcq13", type: "mcq", q: "Which is NOT commonly found in a smart hospital?", options: ["Robotic surgical systems", "Paper-based patient records", "Automated medication dispensers", "Digital patient management systems"], a: 1 },
        { id: "p11-mcq14", type: "mcq", q: "How do smart hospitals improve communication?", options: ["Using telemedicine & apps", "Face- face only", "Paper messaging", "Avoiding electronic communication"], a: 0 },
        { id: "p11-mcq15", type: "mcq", q: "A key feature of smart hospital IT infrastructure:", options: ["Manual data entry", "Advanced cybersecurity", "No internet access", "Basic software only"], a: 1 },
        { id: "p11-mcq16", type: "mcq", q: "Predictive analytics is used to:", options: ["Predict weather", "Forecast medical emergencies", "Manage finances", "Monitor staff"], a: 1 },
        { id: "p11-mcq17", type: "mcq", q: "Common device used in smart hospitals:", options: ["Stethoscope", "Wearable monitors", "Manual cuff", "Logbooks"], a: 1 },
        { id: "p11-mcq18", type: "mcq", q: "How do smart hospitals reduce medical errors?", options: ["Decision support software", "Increase workload", "Avoid tech", "Remove monitoring devices"], a: 0 },
        // Page 12
        { id: "p12-mcq19", type: "mcq", q: "Advantage of digital patient records:", options: ["Less secure", "Easy to access/update", "Only for admin staff", "Require manual filing"], a: 1 },
        { id: "p12-mcq20", type: "mcq", q: "Technology used in smart hospital surgeries:", options: ["Virtual assistants", "Robotic surgical systems", "Blockchain", "Only traditional tools"], a: 1 },
        // T/F with Key (P12/13)
        { id: "p12-tf1", type: "tf", q: "Smart hospitals use AI to assist diagnosis.", a: "True" },
        { id: "p12-tf2", type: "tf", q: "All patient data is stored on paper.", a: "False" },
        { id: "p12-tf3", type: "tf", q: "Robotic surgery is used in some smart hospitals.", a: "True" },
        { id: "p12-tf4", type: "tf", q: "Smart hospitals do not use wearable devices.", a: "False" },
        { id: "p12-tf5", type: "tf", q: "Predictive analytics can foresee health issues.", a: "True" },
        { id: "p12-tf6", type: "tf", q: "Telemedicine is not part of smart hospitals.", a: "False" },
        { id: "p12-tf7", type: "tf", q: "Smart hospitals rely on IoT for real- time monitoring.", a: "True" },
        { id: "p12-tf8", type: "tf", q: "Authorized personnel can access patient data remotely.", a: "True" },
        { id: "p12-tf9", type: "tf", q: "Smart hospitals reduce human error.", a: "True" },
        { id: "p12-tf10", type: "tf", q: "Smart hospitals do not use EHRs.", a: "False" },
      ]
    },
    {
      title: "5. Nursing Informatics",
      questions: [
        // Page 14
        { id: "p14-mcq1", type: "mcq", q: "What is the main goal of Nursing Informatics?", options: ["Replace nurses with computers", "Only store patient data", "Improve communication only", "Improve patient care and decision-making"], a: 3 },
        { id: "p14-mcq2", type: "mcq", q: "When did Nursing Informatics begin to develop in hospitals?", options: ["1940s", "1960s-1970s", "2000s", "1990s"], a: 1 },
        { id: "p14-mcq3", type: "mcq", q: "Which of the following best defines Nursing Informatics?", options: ["Use of technology only", "Integration of nursing and medicine", "Integration of nursing, computer, and information science", "Paper-based documentation"], a: 2 },
        { id: "p14-mcq4", type: "mcq", q: "Which tool allows electronic entry of medication orders?", options: ["Telehealth", "CPOE", "Simulation", "Research tools"], a: 1 },
        { id: "p14-mcq5", type: "mcq", q: "What do Clinical Decision Support Systems (CDSS) provide?", options: ["Entertainment", "Alerts, reminders, and recommendations", "Manual calculations", "Paper reports"], a: 1 },
        { id: "p14-mcq6", type: "mcq", q: "Which function of Nursing Informatics supports staff learning?", options: ["Data management", "Communication", "Education and Training", "Cost reduction"], a: 2 },
        { id: "p14-mcq7", type: "mcq", q: "What is the first level of the DIKW framework?", options: ["Data", "Information", "Knowledge", "Wisdom"], a: 0 },
        // Page 15
        { id: "p15-mcq1", type: "mcq", q: "Which of the following is a future trend in Nursing Informatics?", options: ["More paperwork", "Better accessibility through technology", "Less efficiency", "No use of EHRs"], a: 1 },
        { id: "p15-mcq2", type: "mcq", q: "Which challenge is related to protecting patient data?", options: ["Telemedicine", "Cost containment", "Privacy and security", "Scheduling"], a: 2 },
        { id: "p15-mcq3", type: "mcq", q: "What is the minimum education required to work in Nursing Informatics?", options: ["High school diploma", "BSN (Bachelor of Science in Nursing)", "No degree needed", "Only technical certification"], a: 1 },
        // T/F
        { id: "p15-tf1", type: "tf", q: "Nursing informatics integrates nursing science, computer science, and information science.", a: "True" },
        { id: "p15-tf2", type: "tf", q: "Nursing informatics began in the 1980s.", a: "False" },
        { id: "p15-tf3", type: "tf", q: "The main goal of nursing informatics is to improve patient safety and care quality.", a: "True" },
        { id: "p15-tf4", type: "tf", q: "EHR increases paperwork and slows workflow.", a: "False" },
        { id: "p15-tf5", type: "tf", q: "Decision support systems help nurses make evidence-based decisions.", a: "True" },
        { id: "p15-tf6", type: "tf", q: "Data is interpreted and organized information.", a: "False" },
        { id: "p15-tf7", type: "tf", q: "Telehealth allows remote consultations and follow-up care.", a: "True" },
        { id: "p15-tf8", type: "tf", q: "One function of nursing informatics is quality improvement.", a: "True" },
        { id: "p15-tf9", type: "tf", q: "Future systems in nursing informatics will decrease integration between hospitals.", a: "False" },
        { id: "p15-tf10", type: "tf", q: "Nurses do not need technical skills to work in informatics.", a: "False" },
        // Page 16 (Repeats some concepts, but including as separate questions)
        { id: "p16-mcq1", type: "mcq", q: "Which of the following is not a main function of Nursing Informatics?", options: ["Data management", "Decision support", "Fashion design 🙂", "Communication"], a: 3 },
        { id: "p16-mcq2", type: "mcq", q: "What is one of the main goals of using Electronic Health Records (EHRs)?", options: ["To increase paperwork", "To improve documentation and patient safety", "To replace all healthcare workers", "To slow down workflow"], a: 1 },
        { id: "p16-mcq3", type: "mcq", q: "Which component of Nursing Informatics focuses on collecting and organizing information?", options: ["Nursing science", "Computer science", "Information science", "Behavioral science"], a: 2 },
        { id: "p16-mcq4", type: "mcq", q: "What is a key benefit of Telehealth?", options: ["Limiting access to healthcare", "Providing remote monitoring and consultation", "Replacing hospital visits entirely", "Increasing medical errors"], a: 1 },
        { id: "p16-mcq5", type: "mcq", q: "Which of the following is a challenge for the future of Nursing Informatics?", options: ["Maintaining data privacy and security", "Increasing paperwork", "Reducing technology use", "Avoiding integration between systems"], a: 0 },
        { id: "p16-mcq6", type: "mcq", q: "Which system allows nurses to enter and check medication orders electronically?", options: ["Simulation tools", "CPOE", "Research database", "Communication network"], a: 1 },
        { id: "p16-mcq7", type: "mcq", q: "What does \"Knowledge\" represent in the DIKW framework?", options: ["Unprocessed facts", "Organized data", "Synthesized information identifying relationships", "Random data"], a: 2 },
        { id: "p16-mcq8", type: "mcq", q: "Which role of Nursing Informatics helps improve care quality and safety?", options: ["Quality improvement", "Decoration and design", "Patient entertainment", "Cost calculation only"], a: 0 },
        { id: "p16-mcq9", type: "mcq", q: "What is the minimum educational requirement for a Nursing Informatics specialist?", options: ["Secondary school certificate", "Diploma in computer science", "Bachelor of Science in Nursing (BSN)", "Master's in public health"], a: 2 },
      ]
    },
    {
      title: "6. Informatics security & confidentiality",
      questions: [
        // Page 17
        { id: "p17-mcq1", type: "mcq", q: "What does confidentiality mainly protect?", options: ["The physical security of computers", "The accuracy of data", "Information from unauthorized access", "The speed of a computer system"], a: 2 },
        { id: "p17-mcq2", type: "mcq", q: "Which of the following is a confidentiality threat?", options: ["Authorized login", "Hackers accessing private data", "Regular system updates", "Data backup"], a: 1 },
        { id: "p17-mcq3", type: "mcq", q: "In the Access Control Model, what is the role of a \"subject\"?", options: ["The resource being acted upon", "The set of rules", "The person or program performing the action", "The process of interaction"], a: 2 },
        // Page 18
        { id: "p18-mcq1", type: "mcq", q: "Which of the following is an example of unauthorized activity threatening confidentiality?", options: ["Regular software update", "Local area network misuse", "Daily backup", "Access by an authorized user"], a: 1 },
        { id: "p18-mcq2", type: "mcq", q: "What is the main goal of the \"Security\" principle?", options: ["Allow the patient to change their record", "Protect health information from illegitimate access", "Use information for national priorities", "Punish misuse of information"], a: 1 },
        { id: "p18-mcq3", type: "mcq", q: "What is the primary focus of information security?", options: ["Increasing internet speed", "Protecting confidentiality, integrity, and availability (CIA)", "Developing software", "Creating databases"], a: 1 },
        // Page 19
        { id: "p19-mcq1", type: "mcq", q: "What is the process of identifying weaknesses and deciding how to reduce the danger?", options: ["Risk Mitigation", "Risk Assessment", "Risk Management", "Residual Risk"], a: 2 },
        { id: "p19-mcq2", type: "mcq", q: "What is considered the most vulnerable point in an information system?", options: ["Hardware failure", "Human user", "Network cables", "Software errors"], a: 1 },
        { id: "p19-mcq3", type: "mcq", q: "Which type of analysis is used to calculate the impact of a threat?", options: ["Financial analysis", "Qualitative or quantitative analysis", "Visual analysis", "Behavioral analysis"], a: 1 },
        // Page 20
        { id: "p20-mcq1", type: "mcq", q: "Which model is most commonly used for enforcing confidentiality?", options: ["Clark-Wilson model", "Bell-LaPadula model", "ISO 27001 model", "CIA Triad model"], a: 1 },
        { id: "p20-mcq2", type: "mcq", q: "Which of the following best defines confidentiality?", options: ["Ensuring availability", "Protecting information from unauthorized access", "Preventing communication", "Monitoring users"], a: 1 },
        { id: "p20-mcq3", type: "mcq", q: "Which of the following is considered a subject in the Bell-LaPadula model?", options: ["Files and records", "A person, process, or device", "Security rules", "Network cables"], a: 1 },
        // Page 21
        { id: "p21-mcq1", type: "mcq", q: "The \"Boundaries\" principle refers to:", options: ["Using health information only for health-related purposes", "Allowing information to be shared publicly", "Deleting unnecessary files", "Controlling network traffic"], a: 0 },
        { id: "p21-mcq2", type: "mcq", q: "The \"Public Responsibility\" principle allows disclosure for:", options: ["Private business competition", "Promoting quality care and research", "Increasing profit", "Accessing personal emails"], a: 1 },
        { id: "p21-mcq3", type: "mcq", q: "Accountability in confidentiality principles means:", options: ["Only punishing deliberate disclosure", "Improper disclosure and misuse must be punished", "Ignoring accidental mistakes", "Ignoring system breaches"], a: 1 },
        // Page 22
        { id: "p22-mcq1", type: "mcq", q: "Which of the following is part of information security definitions mentioned in the lecture?", options: ["Protecting intellectual property", "Deleting old files", "Improving internet speed", "Increasing network bandwidth"], a: 0 },
        { id: "p22-mcq2", type: "mcq", q: "Which area is examined during risk assessment according to the lecture?", options: ["Asset management", "Social media trends", "Marketing campaigns", "Sports facilities"], a: 0 },
        { id: "p22-mcq3", type: "mcq", q: "Which step comes after identifying threats and vulnerabilities in risk management?", options: ["Risk treatment (avoid, mitigate, share, accept)", "Hiring new employees", "Designing marketing strategies", "Improving network speed"], a: 0 },
        // Page 23
        { id: "p23-mcq1", type: "mcq", q: "Which of the following is considered a common threat to confidentiality?", options: ["Unprotected downloaded files", "System backup", "Authorized login", "Proper access control"], a: 0 },
        { id: "p23-mcq2", type: "mcq", q: "The Access Control Model organizes the system into:", options: ["People, networks, and devices", "Objects, subjects, and operations", "Data, storage, and bandwidth", "Users, passwords, and firewalls"], a: 1 },
        // Page 24/25 T/F
        { id: "p24-tf1", type: "tf", q: "Businesses use confidentiality to protect their trade secrets.", a: "True" },
        { id: "p24-tf2", type: "tf", q: "Unprotected downloaded files are safe and do not affect confidentiality.", a: "False" },
        { id: "p24-tf3", type: "tf", q: "The Bell-LaPadula model focuses on availability.", a: "False" },
        { id: "p24-tf4", type: "tf", q: "The \"Boundaries\" principle allows using information for any purpose.", a: "False" },
        { id: "p24-tf5", type: "tf", q: "Information security only protects electronic data.", a: "False" },
        { id: "p24-tf6", type: "tf", q: "Risk management is an ongoing and repetitive process.", a: "True" },
        { id: "p25-tf1", type: "tf", q: "Access control is not important in information security risk assessment.", a: "False" },
        { id: "p25-tf2", type: "tf", q: "Risk management ends after implementing controls.", a: "False" },
        { id: "p25-tf3", type: "tf", q: "Risk management is a one-time process.", a: "False" },
        { id: "p25-tf4", type: "tf", q: "The Consumer Control principle gives the patient the right to know who accessed their record.", a: "True" },
      ]
    },
    {
      title: "7. Health care information technology",
      questions: [
        // Page 26
        { id: "p26-mcq1", type: "mcq", q: "Social and cultural barriers includes all EXPECT:", options: ["lack of stakeholder's interest", "less motivation", "anxiety to adapt", "lack of skilled professional human resources"], a: 3 },
        { id: "p26-mcq2", type: "mcq", q: "\"High expenses and long setup time delay implementation\" is a clear example of which barrier to the adoption of healthcare technology?", options: ["Infrastructure Barriers", "Organizational Barriers", "Cost and Time Barriers", "Social and Cultural Barriers"], a: 2 },
        { id: "p26-mcq3", type: "mcq", q: "Which of the following is considered a major barrier to the implementation of Health Information Technology in developing countries?", options: ["High literacy rate among healthcare workers", "Poor or inadequate infrastructure", "Availability of advanced telecommunication systems", "Strong health information system to improve existing services"], a: 1 },
        { id: "p26-mcq4", type: "mcq", q: "Which of the following is a barrier to healthcare technology adoption in the passage?", options: ["Poor internet availability", "Lack of skilled human resources", "Cost and time barriers", "All of the above"], a: 3 },
        // Page 27
        { id: "p27-tf5", type: "tf", q: "Poor internet availability is considered a vital barrier to healthcare technology adoption.", a: "True" },
        { id: "p27-tf6", type: "tf", q: "A Major problem in organizing workshops and trainings and implementation of HIT in under developed countries is financial and time constraint", a: "True" },
        { id: "p27-mcq7", type: "mcq", q: "Which of the following is an entry-level job in healthcare technology systems?", options: ["Clinical Documentation Specialist", "Electronic Health Records (EHR) Specialist", "Patient Access Representative", "Health Information Clerk"], a: 1 },
        { id: "p27-mcq8", type: "mcq", q: "Application Support Specialists usually work in:", options: ["IT departments", "Surgical rooms", "Laboratory units", "Patient wards"], a: 0 },
        { id: "p27-mcq9", type: "mcq", q: "Which job is responsible for converting paper documents to electronic form?", options: ["Clinical Documentation Specialist", "Document Imaging Technician", "Medical Records Analyst", "Patient Access Representative"], a: 1 },
        // Page 28
        { id: "p28-tf10", type: "tf", q: "Entry- level jobs in healthcare technology systems may include both technical IT roles and clerical support roles", a: "True" },
        { id: "p28-tf11", type: "tf", q: "A Medical Records Analyst is the person who scans and converts paper documents into electronic files.", a: "False" },
        { id: "p28-mcq12", type: "mcq", q: "Which of the following best describes a key responsibility of an experienced nurse in healthcare informatics?", options: ["Maintains basic computer skills for daily tasks", "Uses technology to aggregate population-based patient information for decision support", "Follows basic data entry protocols", "Documents patient information in electronic health records"], a: 1 },
        { id: "p28-mcq13", type: "mcq", q: "What is a critical role of an Informatics Nurse Specialist in system safety?", options: ["Installing new software systems", "Managing IT department staff", "Educating non-clinical colleagues about safety risk assessment and mitigation", "Conducting routine hardware maintenance"], a: 2 },
        { id: "p28-mcq14", type: "mcq", q: "Which skill is considered crucial for a Health Information Technician because they work with very sensitive data?", options: ["Creative Problem Solving", "Attention to Detail", "Maintaining Confidentiality", "Ability to Write Well"], a: 2 },
        // Page 29
        { id: "p29-mcq15", type: "mcq", q: "The skill 'Good communication skills' primarily involves:", options: ["Finding innovative solutions to complex technical issues.", "Being able to explain technical issues in simple terms to non-specialists.", "Analyzing patient health records.", "Dealing with people who face technical problems."], a: 1 },
        { id: "p29-mcq16", type: "mcq", q: "Which skill enables the ability to analyze and understand patients' health records?", options: ["Technical Skills", "Analytical Skills", "Customer Service Skills", "Good Communication Skills"], a: 1 },
        { id: "p29-mcq17", type: "mcq", q: "The skill 'Attention to details' is critical for HITS professionals to:", options: ["Communicate effectively.", "Maintain accuracy while entering patient data.", "Use coding systems.", "Solve complex technical issues."], a: 1 },
        // Page 30-33
        { id: "p30-mcq18", type: "mcq", q: "Which of the following is NOT one of the standards of Informatics Nurse Specialist Practice?", options: ["Assessment", "Diagnosis and Issues Identification", "Financial Auditing", "Outcomes Identification"], a: 2 },
        { id: "p30-mcq19", type: "mcq", q: "An Informatics Nurse Specialist evaluating progress toward attaining expected outcomes is fulfilling which standard of practice?", options: ["Standard 4: Planning", "Standard 6: Evaluation", "Standard 8: Education", "Standard 10: Resource Utilization"], a: 1 },
        { id: "p30-mcq20", type: "mcq", q: "Which standard of Informatics Nurse Specialist (INS) Practice involves \"analyzing assessment data to identify problems, needs, and opportunities for improvement\"?", options: ["Planning", "Outcomes Identification", "Diagnosis and Issues Identification", "Evaluation"], a: 2 },
        { id: "p30-mcq21", type: "mcq", q: "The 'Implementation' standard of INS practice primarily focuses on:", options: ["Evaluating progress toward achieving planned outcomes.", "Coordination of activities and managing planned informatics activities.", "Collecting comprehensive data.", "Developing individualized goals."], a: 1 },
        { id: "p31-mcq22", type: "mcq", q: "Which of the following is an advantage of Health Information Systems?", options: ["Increasing the time required for data collection", "Enhancing collaboration among healthcare providers", "Raising the overall cost of healthcare services", "Limiting the ability to analyze patient data"], a: 1 },
        { id: "p31-mcq23", type: "mcq", q: "How do Health Information Systems contribute to population health management?", options: ["By preventing the sharing of medical records between institutions", "By increasing hospitals' operational costs", "By aggregating patient data and analyzing it to identify health trends", "By disabling clinical decision support systems"], a: 2 },
        { id: "p31-mcq24", type: "mcq", q: "The HIT importance Population Health Management primarily involves:", options: ["Managing individual patient health records only", "Using data to track and improve public health", "Training all staff on new software", "Ensuring physical security of health facilities"], a: 1 },
        { id: "p31-mcq25", type: "mcq", q: "The advantage of HIT known as Collaborative Care involves:", options: ["Hiring more administrative staff", "Sharing information between providers to access comprehensive health records", "Providing financial reports to stakeholders only", "Reducing the need for patient interaction"], a: 1 },
        { id: "p32-mcq26", type: "mcq", q: "Which term best describes the use of digital networks to share healthcare data, helping to reduce expenses and improve efficiency?", options: ["Cost Control", "Population Health Management", "Infrastructure", "System Safety"], a: 0 },
        { id: "p32-mcq27", type: "mcq", q: "Healthcare Technology Systems mainly focus on:", options: ["Hardware & software", "Reports for EHR", "Evaluate accuracy of records", "Maintaining facilities information system"], a: 0 },
        { id: "p32-mcq28", type: "mcq", q: "Which role of nursing informatics involves keeping accurate patient records and supporting clinical decisions?", options: ["Education", "Clinical practice", "Administration", "Research"], a: 1 },
        { id: "p32-mcq29", type: "mcq", q: "Which INS role focuses on \"raising awareness about safety risks, applies standards, and ensures safe use of healthcare technologies\"?", options: ["Use Information for Management", "promote health", "Promote System Safety", "Provide Guidance and Education"], a: 2 },
        { id: "p33-mcq30", type: "mcq", q: "One of the primary applications of nursing informatics is to use technology to support what key aspect of patient care?", options: ["Financial billing and coding", "Communication and decision support", "Managing hospital cafeteria", "Scheduling staff vacations"], a: 1 },
      ]
    },
    {
      title: "8. Telehealth",
      questions: [
        // Page 34
        { id: "p34-mcq1", type: "mcq", q: "Telehealth can be defined as:", options: ["Direct physical examination", "Broad variety of virtual health technologies", "Only video calls", "In-person consultation"], a: 1 },
        { id: "p34-mcq2", type: "mcq", q: "Which of the following is NOT a type of telehealth?", options: ["Video conferencing", "Remote patient monitoring", "Home visit by a nurse", "Mobile health"], a: 2 },
        { id: "p34-mcq3", type: "mcq", q: "Video conferencing is mainly used for:", options: ["Surgery", "Consulting and mental health evaluations", "Measuring blood sugar", "Physical rehab"], a: 1 },
        { id: "p34-mcq4", type: "mcq", q: "Remote Patient Monitoring (RPM) helps to:", options: ["Track patient health remotely", "Schedule therapy", "Replace nurses", "Perform lab testing"], a: 0 },
        { id: "p35-mcq5", type: "mcq", q: "Which of the following is an advantage of telehealth?", options: ["Increases travel time", "Saves money & expands access", "Reduces engagement", "Increases crowding"], a: 1 },
        { id: "p35-mcq6", type: "mcq", q: "One disadvantage of telehealth is:", options: ["Limited tech access", "Nurse shortage", "Better continuity", "Better infection control"], a: 0 },
        { id: "p35-mcq7", type: "mcq", q: "Telenursing is defined as:", options: ["IT use for remote nursing", "Online pharmacy", "Emergency communication", "Research method"], a: 0 },
        { id: "p35-mcq8", type: "mcq", q: "Telenursing is closely related to:", options: ["Health economics", "Nursing informatics", "Admin", "Lab tech"], a: 1 },
        { id: "p35-mcq9", type: "mcq", q: "Nurse working from home is example of:", options: ["Traditional nursing", "Tele-nursing advantage", "Bedside nursing", "Emergency care"], a: 1 },
        { id: "p36-mcq10", type: "mcq", q: "Benefit of telenursing for nurses:", options: ["Increased workload", "Higher job satisfaction", "Less flexibility", "More travel"], a: 1 },
        { id: "p36-mcq11", type: "mcq", q: "Telenursing application:", options: ["School health", "Home care for chronic patients", "Hospital rounds", "Pharmacy management"], a: 1 },
        { id: "p36-mcq12", type: "mcq", q: "Telephone triage involves:", options: ["Physical exam", "Symptom assessment over phone", "Medication delivery", "Nurse travel"], a: 1 },
        { id: "p36-mcq13", type: "mcq", q: "Main goal of telephone triage:", options: ["Increase visits", "Reduce ER overcrowding", "Replace ER", "Delay treatment"], a: 1 },
        { id: "p37-mcq14", type: "mcq", q: "Telepsychiatry useful in:", options: ["Abundant care areas", "Rural/crisis zones", "Therapy centers", "Labs"], a: 1 },
        { id: "p37-mcq15", type: "mcq", q: "During COVID-19, telehealth promoted to:", options: ["Increase in-person visits", "Reduce infection spread", "Stop remote care", "Train staff"], a: 1 },
        { id: "p37-mcq16", type: "mcq", q: "Which technology allows nurses to assess patients through live interaction?", options: ["Digital transmission", "Video conferencing", "Remote patient monitoring", "Mobile health"], a: 1 },
        { id: "p37-mcq17", type: "mcq", q: "What is a disadvantage of telehealth regarding continuity of care?", options: ["Different providers each visit", "Improved follow-up", "Enhanced engagement", "Reduced waiting time"], a: 0 },
        { id: "p38-mcq18", type: "mcq", q: "Which branch of informatics supports telenursing development?", options: ["Medical economics", "Nursing informatics", "Health communication", "Data analytics"], a: 1 },
        { id: "p38-mcq19", type: "mcq", q: "What is one main legal issue in telenursing practice?", options: ["High internet speed", "Nurse licensure across states", "Long waiting time", "Too many nurses"], a: 1 },
        { id: "p38-mcq20", type: "mcq", q: "Home care telenursing can support patients with:", options: ["Chronic diseases", "Temporary visitors", "Hospitalized patients", "Healthy children"], a: 0 },
        { id: "p38-mcq21", type: "mcq", q: "Which of the following improves infection control in telehealth?", options: ["Increased travel", "Reduced PPE use", "More in-person care", "Larger hospitals"], a: 1 },
        { id: "p38-mcq22", type: "mcq", q: "Telephone triage nurses mainly provide:", options: ["Medicine delivery", "Health advice and symptom evaluation", "Lab tests", "Surgery"], a: 1 },
        { id: "p39-mcq23", type: "mcq", q: "What population benefits most from telepsychiatry?", options: ["Urban professionals", "Rural or crisis areas", "Students only", "Hospital administrators"], a: 1 },
        { id: "p39-mcq24", type: "mcq", q: "During pandemics, telehealth helps to:", options: ["Increase crowding", "Reduce infection risk", "Decrease social distancing", "Close clinics"], a: 1 },
        { id: "p39-mcq25", type: "mcq", q: "Ethical issues in telenursing include:", options: ["Patient autonomy and privacy", "Nurse salary", "Hospital management", "Data storage size"], a: 0 },
        // T/F
        { id: "p39-tf26", type: "tf", q: "Telehealth reduces PPE use because it limits in-person contact.", a: "True" },
        { id: "p39-tf27", type: "tf", q: "Telenursing cannot be used for home care patients.", a: "False" },
        { id: "p39-tf28", type: "tf", q: "Telephone triage aims to increase hospital emergency visits.", a: "False" },
        { id: "p39-tf29", type: "tf", q: "Nursing informatics supports the development of telenursing.", a: "True" },
        { id: "p40-tf30", type: "tf", q: "Telepsychiatry helps provide care in areas with limited mental health access.", a: "True" },
      ]
    }
  ];

  const handleAnswer = (questionId, selectedOption) => {
    setAnswers(prev => ({
      ...prev,
      [questionId]: selectedOption
    }));
  };

  const getScoreForSection = (sectionIndex) => {
    const sectionQuestions = sections[sectionIndex].questions;
    let score = 0;
    sectionQuestions.forEach(q => {
      const userAnswer = answers[q.id];
      if (userAnswer === undefined) return;
      if (userAnswer === q.a) score++;
    });
    return { score, total: sectionQuestions.length };
  };

  const resetQuiz = () => {
    if (window.confirm("Reset all your answers and progress?")) {
      setAnswers({});
      setBookmarks([]);
      setActiveSection(0);
      setViewMode('normal');
    }
  };

  // Feature: Bookmark logic
  const toggleBookmark = (id) => {
    setBookmarks(prev => prev.includes(id) ? prev.filter(bId => bId !== id) : [...prev, id]);
  };

  // Feature: Gather mistakes
  const getAllMistakes = () => {
    const mistakes = [];
    sections.forEach(s => {
      s.questions.forEach(q => {
        if (answers[q.id] !== undefined && answers[q.id] !== q.a) {
          mistakes.push(q);
        }
      });
    });
    return mistakes;
  };

  const getBookmarkedQuestions = () => {
    const bookmarked = [];
    sections.forEach(s => {
      s.questions.forEach(q => {
        if (bookmarks.includes(q.id)) {
          bookmarked.push(q);
        }
      });
    });
    return bookmarked;
  };

  // Decide which questions to show
  let displayedQuestions = [];
  let currentTitle = "";

  if (viewMode === 'bookmarks') {
    displayedQuestions = getBookmarkedQuestions();
    currentTitle = "Bookmarked Questions";
  } else if (viewMode === 'mistakes') {
    displayedQuestions = getAllMistakes();
    currentTitle = "Review Mistakes";
  } else {
    displayedQuestions = sections[activeSection].questions;
    currentTitle = sections[activeSection].title;
  }

  return (
    <div className="flex flex-col md:flex-row h-screen bg-gray-50 text-gray-800 font-sans">
      {/* Sidebar Navigation */}
      <div className={`fixed inset-y-0 left-0 transform ${sidebarOpen ? 'translate-x-0' : '-translate-x-full'} md:relative md:translate-x-0 transition duration-200 ease-in-out z-20 w-80 bg-white border-r border-gray-200 shadow-lg md:shadow-none flex flex-col`}>
        <div className="p-6 border-b border-gray-100 flex items-center justify-between">
          <div className="flex items-center space-x-2 text-indigo-700 font-bold text-xl">
            <BookOpen className="w-6 h-6" />
            <span>MedTech Quiz</span>
          </div>
          <button onClick={() => setSidebarOpen(false)} className="md:hidden text-gray-500">
            <XCircle className="w-6 h-6" />
          </button>
        </div>
        
        <div className="flex-1 overflow-y-auto py-4">
          {/* Smart Review Section */}
          <div className="px-6 mb-2 text-xs font-bold text-gray-400 uppercase tracking-wider">Smart Review</div>
          <button
            onClick={() => { setViewMode('bookmarks'); setSidebarOpen(false); }}
            className={`w-full text-left px-6 py-3 flex items-center space-x-3 transition-colors ${viewMode === 'bookmarks' ? 'bg-yellow-50 text-yellow-700 border-l-4 border-yellow-500' : 'hover:bg-gray-50'}`}
          >
            <Bookmark className="w-4 h-4" />
            <span className="text-sm font-medium">Bookmarks ({bookmarks.length})</span>
          </button>
          <button
            onClick={() => { setViewMode('mistakes'); setSidebarOpen(false); }}
            className={`w-full text-left px-6 py-3 flex items-center space-x-3 transition-colors ${viewMode === 'mistakes' ? 'bg-red-50 text-red-700 border-l-4 border-red-500' : 'hover:bg-gray-50'}`}
          >
            <AlertCircle className="w-4 h-4" />
            <span className="text-sm font-medium">My Mistakes ({getAllMistakes().length})</span>
          </button>

          <div className="px-6 mt-6 mb-2 text-xs font-bold text-gray-400 uppercase tracking-wider">Chapters</div>
          {sections.map((section, idx) => {
            const { score, total } = getScoreForSection(idx);
            const answeredCount = sections[idx].questions.filter(q => answers[q.id] !== undefined).length;
            const isComplete = answeredCount === total && total > 0;
            return (
              <button
                key={idx}
                onClick={() => {
                  setActiveSection(idx);
                  setViewMode('normal');
                  setSidebarOpen(false);
                }}
                className={`w-full text-left px-6 py-4 hover:bg-gray-50 transition-colors border-l-4 ${activeSection === idx && viewMode === 'normal' ? 'border-indigo-600 bg-indigo-50' : 'border-transparent'}`}
              >
                <div className="flex justify-between items-center mb-1">
                  <span className={`font-medium text-sm ${activeSection === idx && viewMode === 'normal' ? 'text-indigo-800' : 'text-gray-700'}`}>
                    {section.title}
                  </span>
                  {isComplete && <CheckCircle className="w-4 h-4 text-green-500" />}
                </div>
                <div className="flex items-center space-x-2 text-xs text-gray-500">
                  <span>{score}/{total} Correct</span>
                  <div className="flex-1 h-1.5 bg-gray-200 rounded-full overflow-hidden">
                    <div 
                      className="h-full bg-green-500 transition-all duration-500"
                      style={{ width: `${total > 0 ? (score/total)*100 : 0}%` }}
                    ></div>
                  </div>
                </div>
              </button>
            );
          })}
        </div>

        <div className="p-4 border-t border-gray-100 bg-gray-50">
           <button 
            onClick={resetQuiz}
            className="flex items-center justify-center w-full px-4 py-2 text-sm text-red-600 bg-white border border-red-200 rounded-md hover:bg-red-50 transition-colors"
          >
            <RefreshCw className="w-4 h-4 mr-2" />
            Reset Quiz
          </button>
        </div>
      </div>

      {/* Main Content */}
      <div className="flex-1 flex flex-col h-screen overflow-hidden">
        {/* Mobile Header */}
        <div className="md:hidden bg-white border-b border-gray-200 p-4 flex items-center justify-between shadow-sm z-10">
          <div className="font-bold text-lg text-gray-800 truncate">{currentTitle}</div>
          <button onClick={() => setSidebarOpen(true)} className="text-gray-600">
            <Menu className="w-6 h-6" />
          </button>
        </div>

        {/* Scrollable Question Area */}
        <div className="flex-1 overflow-y-auto p-4 md:p-8 bg-gray-50">
          <div className="max-w-3xl mx-auto">
            <div className="mb-6">
              <h1 className="text-2xl font-bold text-gray-900 mb-2">{currentTitle}</h1>
              <p className="text-gray-500 text-sm">
                {displayedQuestions.length} Questions {viewMode !== 'normal' ? 'found' : ''}
              </p>
            </div>

            {displayedQuestions.length === 0 && (
              <div className="bg-white rounded-xl p-12 text-center border border-gray-200 shadow-sm">
                <div className="inline-flex items-center justify-center w-16 h-16 rounded-full bg-gray-50 text-gray-400 mb-4">
                  {viewMode === 'bookmarks' ? <Bookmark className="w-8 h-8" /> : <CheckCircle className="w-8 h-8" />}
                </div>
                <h3 className="text-lg font-medium text-gray-900 mb-1">
                  {viewMode === 'bookmarks' ? "No bookmarks yet" : "No mistakes to review"}
                </h3>
                <p className="text-gray-500">
                  {viewMode === 'bookmarks' ? "Star questions to save them for later review." : "Questions you answer incorrectly will appear here."}
                </p>
              </div>
            )}

            <div className="space-y-6 pb-20">
              {displayedQuestions.map((q, index) => {
                const userAnswer = answers[q.id];
                const isAnswered = userAnswer !== undefined;
                const isCorrect = isAnswered && userAnswer === q.a;
                const isBookmarked = bookmarks.includes(q.id);

                return (
                  <div key={q.id} className={`bg-white rounded-xl shadow-sm border transition-all duration-300 relative ${isAnswered ? (isCorrect ? 'border-green-200 shadow-green-50' : 'border-red-200 shadow-red-50') : 'border-gray-200 hover:shadow-md'}`}>
                    
                    {/* Bookmark Toggle */}
                    <button 
                      onClick={() => toggleBookmark(q.id)}
                      className={`absolute top-4 right-4 p-2 rounded-full transition-colors ${isBookmarked ? 'text-yellow-500 bg-yellow-50' : 'text-gray-300 hover:bg-gray-50 hover:text-gray-400'}`}
                    >
                      <Star className={`w-5 h-5 ${isBookmarked ? 'fill-current' : ''}`} />
                    </button>

                    <div className="p-6">
                      <div className="flex items-start space-x-4">
                        <span className="flex-shrink-0 flex items-center justify-center w-8 h-8 rounded-full bg-indigo-100 text-indigo-600 font-bold text-sm">
                          {viewMode === 'normal' ? index + 1 : '•'}
                        </span>
                        <div className="flex-1 pr-10">
                          <h3 className="text-lg font-medium text-gray-900 mb-4 leading-relaxed">
                            {q.q}
                          </h3>
                          
                          <div className="space-y-3">
                            {q.type === 'tf' ? (
                              <div className="flex space-x-4">
                                {['True', 'False'].map((opt) => {
                                  const isSelected = userAnswer === opt;
                                  const isCorrectOption = q.a === opt;
                                  
                                  let btnClass = "flex-1 py-3 px-4 rounded-lg border font-medium transition-all duration-200 text-center ";
                                  if (isAnswered) {
                                    if (isSelected && isCorrect) btnClass += "bg-green-100 border-green-500 text-green-800";
                                    else if (isSelected && !isCorrect) btnClass += "bg-red-100 border-red-500 text-red-800";
                                    else if (!isSelected && isCorrectOption) btnClass += "bg-green-50 border-green-200 text-green-700 opacity-70";
                                    else btnClass += "bg-gray-50 border-gray-100 text-gray-400 opacity-50 cursor-not-allowed";
                                  } else {
                                    btnClass += "bg-white border-gray-200 hover:border-indigo-500 hover:bg-indigo-50 text-gray-600 hover:text-indigo-700 cursor-pointer";
                                  }

                                  return (
                                    <button
                                      key={opt}
                                      onClick={() => !isAnswered && handleAnswer(q.id, opt)}
                                      disabled={isAnswered}
                                      className={btnClass}
                                    >
                                      {opt}
                                    </button>
                                  );
                                })}
                              </div>
                            ) : (
                              <div className="grid grid-cols-1 gap-3">
                                {q.options.map((opt, i) => {
                                  const isSelected = userAnswer === i;
                                  const isCorrectOption = q.a === i;
                                  
                                  let btnClass = "w-full text-left p-4 rounded-lg border transition-all duration-200 flex items-center ";
                                  
                                  if (isAnswered) {
                                    if (isSelected && isCorrect) btnClass += "bg-green-50 border-green-500 ring-1 ring-green-500";
                                    else if (isSelected && !isCorrect) btnClass += "bg-red-50 border-red-500 ring-1 ring-red-500";
                                    else if (!isSelected && isCorrectOption) btnClass += "bg-green-50 border-green-300";
                                    else btnClass += "bg-gray-50 border-gray-100 opacity-50";
                                  } else {
                                    btnClass += "bg-white border-gray-200 hover:border-indigo-400 hover:bg-indigo-50 cursor-pointer";
                                  }

                                  return (
                                    <button
                                      key={i}
                                      onClick={() => !isAnswered && handleAnswer(q.id, i)}
                                      disabled={isAnswered}
                                      className={btnClass}
                                    >
                                      <div className={`w-5 h-5 rounded-full border mr-3 flex items-center justify-center ${
                                        isAnswered && (isSelected || isCorrectOption) 
                                          ? (isCorrectOption ? 'border-green-500 bg-green-500 text-white' : 'border-red-500 bg-red-500 text-white')
                                          : 'border-gray-300'
                                      }`}>
                                        {isAnswered && (isSelected || isCorrectOption) && (
                                          isCorrectOption ? <CheckCircle className="w-3 h-3" /> : <XCircle className="w-3 h-3" />
                                        )}
                                      </div>
                                      <span className={isAnswered && isCorrectOption ? "font-medium text-green-900" : "text-gray-700"}>
                                        {opt}
                                      </span>
                                    </button>
                                  );
                                })}
                              </div>
                            )}
                          </div>
                          
                          {isAnswered && !isCorrect && (
                            <div className="mt-4 p-3 bg-red-50 border border-red-100 rounded-lg flex items-start text-red-800 text-sm animate-fade-in">
                              <XCircle className="w-5 h-5 mr-2 flex-shrink-0" />
                              <div>
                                <span className="font-bold">Incorrect.</span> The correct answer is: <span className="font-bold">
                                  {q.type === 'tf' ? q.a : q.options[q.a]}
                                </span>
                              </div>
                            </div>
                          )}
                        </div>
                      </div>
                    </div>
                  </div>
                );
              })}
            </div>

            {/* Next Section Button */}
            {viewMode === 'normal' && activeSection < sections.length - 1 && (
              <div className="flex justify-end pb-10">
                <button
                  onClick={() => {
                    setActiveSection(activeSection + 1);
                    window.scrollTo({ top: 0, behavior: 'smooth' });
                  }}
                  className="flex items-center px-6 py-3 bg-indigo-600 text-white font-medium rounded-lg shadow-lg hover:bg-indigo-700 transition-colors"
                >
                  Next Section <ChevronRight className="w-5 h-5 ml-2" />
                </button>
              </div>
            )}
          </div>
        </div>
      </div>
    </div>
  );
};

export default QuizApp;

