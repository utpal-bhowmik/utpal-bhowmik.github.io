[student_analytics_dashboard.html](https://github.com/user-attachments/files/29461571/student_analytics_dashboard.html)
<!DOCTYPE html>
<html lang="en" class="h-full bg-slate-900">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Student Performance & Engagement Dashboard</title>
  <!-- Tailwind CSS CDN -->
  <script src="https://cdn.tailwindcss.com"></script>
  <script>
    tailwind.config = {
      theme: {
        extend: {
          colors: {
            slate: {
              850: '#1e293b/80',
            }
          }
        }
      }
    }
  </script>
</head>
<body class="min-h-screen bg-slate-900 text-slate-100 font-sans p-4 md:p-8">

  <!-- Main Container -->
  <div class="max-w-7xl mx-auto">
    
    <!-- Header section -->
    <header class="mb-8 flex flex-col md:flex-row md:items-center md:justify-between border-b border-slate-800 pb-6">
      <div>
        <div class="flex items-center gap-3">
          <div class="bg-indigo-600 text-white p-2 rounded-lg">
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 14l9-5-9-5-9 5 9 5z" />
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 14l9-5-9-5-9 5 9 5zm0 0l-9 5 9 5 9-5-9-5zm0 0v6" />
            </svg>
          </div>
          <h1 class="text-2xl md:text-3xl font-extrabold tracking-tight text-white">
            Student Performance & Engagement Dashboard
          </h1>
        </div>
        <p class="text-slate-400 mt-1 text-sm md:text-base">
          Live evaluation analytics platform representing active academic terms.
        </p>
      </div>
      
      <!-- Reset Filters Quick Button -->
      <button 
        id="clearFiltersBtn"
        onclick="handleResetFilters()"
        class="hidden mt-4 md:mt-0 px-4 py-2 bg-indigo-500/10 hover:bg-indigo-500/20 text-indigo-400 border border-indigo-500/20 rounded-lg text-sm font-semibold transition-all duration-150 flex items-center justify-center gap-2"
      >
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M4 4v5h.582m15.356 2A8.001 8.001 0 1121.21 15M13.5 10.5L21 3" />
        </svg>
        Clear Filters
      </button>
    </header>

    <!-- Control Panel / Slicers -->
    <section class="bg-slate-800/50 border border-slate-800 rounded-xl p-4 md:p-6 mb-8 shadow-xl">
      <h2 class="text-sm font-bold text-slate-300 uppercase tracking-wider mb-4 flex items-center gap-2">
        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-indigo-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
          <path strokeLinecap="round" strokeLinejoin="round" strokeWidth={2} d="M3 4a1 1 0 011-1h16a1 1 0 011 1v2.586a1 1 0 01-.293.707l-6.414 6.414a1 1 0 00-.293.707V17l-4 4v-6.586a1 1 0 00-.293-.707L3.293 7.293A1 1 0 013 6.586V4z" />
        </svg>
        Interactive Slicers & Filters
      </h2>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
        
        <!-- Major Filter -->
        <div class="flex flex-col gap-1.5">
          <label class="text-xs font-semibold text-slate-400">Academic Major</label>
          <select 
            id="majorFilter" 
            onchange="handleFilterChange()"
            class="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:ring-2 focus:ring-indigo-500 transition duration-150 cursor-pointer"
          >
            <!-- Options dynamically populated by JS -->
          </select>
        </div>

        <!-- Housing Filter -->
        <div class="flex flex-col gap-1.5">
          <label class="text-xs font-semibold text-slate-400">Housing Arrangement</label>
          <select 
            id="housingFilter" 
            onchange="handleFilterChange()"
            class="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:ring-2 focus:ring-indigo-500 transition duration-150 cursor-pointer"
          >
            <!-- Options dynamically populated by JS -->
          </select>
        </div>

        <!-- Tuition Status Filter -->
        <div class="flex flex-col gap-1.5">
          <label class="text-xs font-semibold text-slate-400">Tuition Status</label>
          <select 
            id="tuitionFilter" 
            onchange="handleFilterChange()"
            class="w-full bg-slate-900 border border-slate-700 rounded-lg px-3 py-2.5 text-sm text-white focus:outline-none focus:ring-2 focus:ring-indigo-500 transition duration-150 cursor-pointer"
          >
            <!-- Options dynamically populated by JS -->
          </select>
        </div>

      </div>
    </section>

    <!-- KPI Cards section -->
    <section class="grid grid-cols-2 lg:grid-cols-4 gap-4 mb-8">
      
      <!-- Total Count Card -->
      <div class="bg-slate-800/40 border border-slate-800 p-5 rounded-xl flex items-center justify-between shadow-lg">
        <div>
          <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Filtered Cohort</p>
          <h3 id="kpiFilteredCohort" class="text-2xl md:text-3xl font-black text-white mt-1">0</h3>
          <p class="text-[10px] text-slate-500 mt-1">out of 10 students total</p>
        </div>
        <div class="p-3 bg-blue-500/10 text-blue-400 rounded-lg">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M17 20h5v-2a3 3 0 00-5.356-1.857M17 20H7m10 0v-2c0-.656-.126-1.283-.356-1.857M7 20H2v-2a3 3 0 015.356-1.857M7 20v-2c0-.656.126-1.283.356-1.857m0 0a5.002 5.002 0 019.288 0M15 7a3 3 0 11-6 0 3 3 0 016 0zm6 3a2 2 0 11-4 0 2 2 0 014 0zM7 10a2 2 0 11-4 0 2 2 0 014 0z" />
          </svg>
        </div>
      </div>

      <!-- Avg GPA Card -->
      <div class="bg-slate-800/40 border border-slate-800 p-5 rounded-xl flex items-center justify-between shadow-lg">
        <div>
          <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Average GPA</p>
          <h3 id="kpiAvgGpa" class="text-2xl md:text-3xl font-black text-emerald-400 mt-1">0.00</h3>
          <p class="text-[10px] text-emerald-500 mt-1">Scale of 0.00 - 4.00</p>
        </div>
        <div class="p-3 bg-emerald-500/10 text-emerald-400 rounded-lg">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M9 12l2 2 4-4M7.835 4.697a3.42 3.42 0 001.946-.806 3.42 3.42 0 014.438 0 3.42 3.42 0 001.946.806 3.42 3.42 0 013.138 3.138 3.42 3.42 0 00.806 1.946 3.42 3.42 0 010 4.438 3.42 3.42 0 00-.806 1.946 3.42 3.42 0 01-3.138 3.138 3.42 3.42 0 00-1.946.806 3.42 3.42 0 01-4.438 0 3.42 3.42 0 00-1.946-.806 3.42 3.42 0 01-3.138-3.138 3.42 3.42 0 00-.806-1.946 3.42 3.42 0 010-4.438 3.42 3.42 0 00.806-1.946 3.42 3.42 0 013.138-3.138z" />
          </svg>
        </div>
      </div>

      <!-- Avg Attendance Card -->
      <div class="bg-slate-800/40 border border-slate-800 p-5 rounded-xl flex items-center justify-between shadow-lg">
        <div>
          <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Avg Attendance</p>
          <h3 id="kpiAvgAttendance" class="text-2xl md:text-3xl font-black text-indigo-400 mt-1">0.0%</h3>
          <p class="text-[10px] text-indigo-500 mt-1">Classroom engagement</p>
        </div>
        <div class="p-3 bg-indigo-500/10 text-indigo-400 rounded-lg">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M8 7V3m8 4V3m-9 8h10M5 21h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v12a2 2 0 002 2z" />
          </svg>
        </div>
      </div>

      <!-- At Risk Card -->
      <div class="bg-slate-800/40 border border-slate-800 p-5 rounded-xl flex items-center justify-between shadow-lg">
        <div>
          <p class="text-xs font-semibold text-slate-400 uppercase tracking-wider">Students At Risk</p>
          <h3 id="kpiAtRisk" class="text-2xl md:text-3xl font-black mt-1 text-slate-400">0</h3>
          <p class="text-[10px] text-slate-500 mt-1">GPA &lt; 2.5 or Att &lt; 75%</p>
        </div>
        <div id="kpiAtRiskIconWrapper" class="p-3 rounded-lg bg-slate-700/20 text-slate-500">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M12 9v2m0 4h.01m-6.938 4h13.856c1.54 0 2.502-1.667 1.732-3L13.732 4c-.77-1.333-2.694-1.333-3.464 0L3.34 16c-.77 1.333.192 3 1.732 3z" />
          </svg>
        </div>
      </div>

    </section>

    <!-- Main Charts & Visualizations Area -->
    <section class="grid grid-cols-1 xl:grid-cols-3 gap-6 mb-8">
      
      <!-- Visualization 1: Scatter Plot (Study Hours vs GPA) -->
      <div class="bg-slate-800/30 border border-slate-800 p-6 rounded-xl shadow-lg xl:col-span-2">
        <div class="flex justify-between items-start mb-6">
          <div>
            <h3 class="text-md font-bold text-white">Correlation Analysis</h3>
            <p class="text-xs text-slate-400">Study Hours (X-Axis) vs. Academic GPA (Y-Axis)</p>
          </div>
          <span class="text-[10px] bg-slate-700/60 border border-slate-700 px-2 py-1 rounded text-slate-300 font-semibold uppercase tracking-wider">
            Scatter Plot
          </span>
        </div>

        <div class="relative h-64 border-l border-b border-slate-700 ml-8 mb-6 mt-4">
          <!-- Grid Lines -->
          <div class="absolute left-0 right-0 top-0 border-t border-slate-800/80"></div>
          <div class="absolute left-0 right-0 top-1/4 border-t border-slate-800/80"></div>
          <div class="absolute left-0 right-0 top-2/4 border-t border-slate-800/80"></div>
          <div class="absolute left-0 right-0 top-3/4 border-t border-slate-800/80"></div>

          <!-- Y Axis Labels -->
          <div class="absolute -left-8 top-0 text-[10px] text-slate-500">4.0</div>
          <div class="absolute -left-8 top-1/4 text-[10px] text-slate-500">3.0</div>
          <div class="absolute -left-8 top-2/4 text-[10px] text-slate-500">2.0</div>
          <div class="absolute -left-8 top-3/4 text-[10px] text-slate-500">1.0</div>
          <div class="absolute -left-8 -bottom-1 text-[10px] text-slate-500">0.0</div>

          <!-- X Axis Labels -->
          <div class="absolute left-0 -bottom-6 text-[10px] text-slate-500">0 hrs</div>
          <div class="absolute left-1/4 -bottom-6 -translate-x-1/2 text-[10px] text-slate-500">6.25 hrs</div>
          <div class="absolute left-2/4 -bottom-6 -translate-x-1/2 text-[10px] text-slate-500">12.5 hrs</div>
          <div class="absolute left-3/4 -bottom-6 -translate-x-1/2 text-[10px] text-slate-500">18.75 hrs</div>
          <div class="absolute right-0 -bottom-6 text-[10px] text-slate-500">25 hrs</div>

          <!-- Scatter Points Container -->
          <div id="scatterPoints" class="absolute inset-0 overflow-visible">
            <!-- Rendered via JavaScript -->
          </div>
        </div>
        
        <div class="flex justify-center flex-wrap gap-4 md:gap-6 mt-4">
          <div class="flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-emerald-400"></span>
            <span class="text-[11px] text-slate-400">High Performer (GPA &gt;= 3.5)</span>
          </div>
          <div class="flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-indigo-400"></span>
            <span class="text-[11px] text-slate-400">Average Performance</span>
          </div>
          <div class="flex items-center gap-1.5">
            <span class="w-2.5 h-2.5 rounded-full bg-rose-500"></span>
            <span class="text-[11px] text-slate-400">Needs Support (&lt; 2.5)</span>
          </div>
        </div>
      </div>

      <!-- Visualization 2: Distribution of Cohort by Major -->
      <div class="bg-slate-800/30 border border-slate-800 p-6 rounded-xl shadow-lg flex flex-col justify-between">
        <div>
          <div class="flex justify-between items-start mb-6">
            <div>
              <h3 class="text-md font-bold text-white">Cohort Distribution</h3>
              <p class="text-xs text-slate-400">Distribution by Major Department</p>
            </div>
            <span class="text-[10px] bg-slate-700/60 border border-slate-700 px-2 py-1 rounded text-slate-300 font-semibold uppercase tracking-wider">
              Distribution
            </span>
          </div>

          <!-- Custom Bar Breakdown Container -->
          <div id="majorDistributionList" class="space-y-4 my-2">
            <!-- Dynamically populated via JavaScript -->
          </div>
        </div>

        <div class="text-[11px] text-slate-400 mt-6 bg-indigo-500/10 border border-slate-800/40 p-3 rounded-lg flex gap-2 items-start">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 text-indigo-400 shrink-0 mt-0.5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M13 16h-1v-4h-1m1-4h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <span>Click any student in the directory below to view deep academic performance profiles directly inside the side drawer.</span>
        </div>
      </div>

    </section>

    <!-- Grid: Directory Table & Quick Viewer -->
    <section class="grid grid-cols-1 lg:grid-cols-3 gap-6 items-start">
      
      <!-- Main Data Directory Table -->
      <div class="bg-slate-800/30 border border-slate-800 rounded-xl shadow-lg p-6 lg:col-span-2 overflow-hidden">
        <div class="flex flex-col md:flex-row md:items-center justify-between gap-4 mb-6">
          <div>
            <h3 class="text-lg font-bold text-white flex items-center gap-2">
              Student Directory 
              <span id="cohortCountBadge" class="text-xs font-normal text-slate-400">(0 records)</span>
            </h3>
            <p class="text-xs text-slate-400">Academic ledger of enrolled students.</p>
          </div>
        </div>

        <!-- Directory Content -->
        <div class="overflow-x-auto" id="tableWrapper">
          <table class="w-full text-left border-collapse">
            <thead>
              <tr class="border-b border-slate-800 text-[11px] font-bold text-slate-400 uppercase tracking-wider">
                <th class="pb-3 pl-3">ID</th>
                <th class="pb-3">Major</th>
                <th class="pb-3 text-center">GPA</th>
                <th class="pb-3 text-center">Attendance</th>
                <th class="pb-3 text-center">Study Hrs/Wk</th>
                <th class="pb-3">Status</th>
                <th class="pb-3 pr-3 text-right">Profile</th>
              </tr>
            </thead>
            <tbody id="directoryTableBody" class="divide-y divide-slate-850">
              <!-- Rendered via JavaScript -->
            </tbody>
          </table>
        </div>

        <!-- Empty State -->
        <div id="emptyState" class="hidden text-center py-12 bg-slate-900/50 border border-dashed border-slate-800 rounded-xl">
          <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto h-12 w-12 text-slate-600 mb-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M9.172 16.172a4 4 0 015.656 0M9 10h.01M15 10h.01M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
          </svg>
          <h4 class="text-slate-300 font-semibold text-sm">No Results Match Selected Filters</h4>
          <p class="text-xs text-slate-500 mt-1">Try resetting or loosening your dashboard filters.</p>
          <button 
            onclick="handleResetFilters()"
            class="mt-4 px-3.5 py-1.5 bg-indigo-600 hover:bg-indigo-500 text-white font-medium text-xs rounded-lg transition-colors"
          >
            Reset All Filters
          </button>
        </div>
      </div>

      <!-- Quick Insights Side Drawer -->
      <div class="bg-slate-800/30 border border-slate-800 p-6 rounded-xl shadow-lg">
        <h3 class="text-md font-bold text-white mb-4 flex items-center gap-2">
          <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-indigo-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M11 3.055A9.003 9.003 0 1020.945 13H11V3.055z" />
            <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M20.488 9H15V3.512A9.025 9.025 0 0120.488 9z" />
          </svg>
          Selected Profile Analyzer
        </h3>

        <!-- Profile container filled dynamically by JS -->
        <div id="profileAnalyzerContainer">
          <!-- Rendered via JavaScript -->
        </div>
      </div>

    </section>

  </div>

  <!-- JavaScript Logic -->
  <script>
    // Raw Student Dataset
    const RAW_STUDENT_DATA = [
      { studentId: "STU0001", major: "Computer Science", attendance: 95.2, studyHours: 18.5, lmsLogins: 22, libraryVisits: 12, gpa: 3.85, tuition: "Paid", housing: "On-Campus" },
      { studentId: "STU0002", major: "Business", attendance: 88.5, studyHours: 12.0, lmsLogins: 14, libraryVisits: 5, gpa: 3.12, tuition: "Paid", housing: "Off-Campus" },
      { studentId: "STU0003", major: "Computer Science", attendance: 62.1, studyHours: 4.5, lmsLogins: 6, libraryVisits: 1, gpa: 1.95, tuition: "Overdue", housing: "Off-Campus" },
      { studentId: "STU0004", major: "Biology", attendance: 91.0, studyHours: 16.2, lmsLogins: 18, libraryVisits: 9, gpa: 3.45, tuition: "Paid", housing: "On-Campus" },
      { studentId: "STU0005", major: "Mechanical Engineering", attendance: 78.4, studyHours: 11.5, lmsLogins: 12, libraryVisits: 4, gpa: 2.78, tuition: "Pending", housing: "On-Campus" },
      { studentId: "STU0006", major: "Business", attendance: 99.1, studyHours: 22.0, lmsLogins: 25, libraryVisits: 15, gpa: 4.00, tuition: "Paid", housing: "On-Campus" },
      { studentId: "STU0007", major: "Art History", attendance: 84.3, studyHours: 8.5, lmsLogins: 10, libraryVisits: 8, gpa: 2.89, tuition: "Paid", housing: "Off-Campus" },
      { studentId: "STU0008", major: "Biology", attendance: 55.0, studyHours: 3.1, lmsLogins: 4, libraryVisits: 0, gpa: 1.52, tuition: "Overdue", housing: "Off-Campus" },
      { studentId: "STU0009", major: "Computer Science", attendance: 93.4, studyHours: 19.0, lmsLogins: 21, libraryVisits: 11, gpa: 3.78, tuition: "Paid", housing: "On-Campus" },
      { studentId: "STU0010", major: "Mechanical Engineering", attendance: 81.2, studyHours: 10.8, lmsLogins: 13, libraryVisits: 3, gpa: 2.65, tuition: "Pending", housing: "Off-Campus" }
    ];

    // State Variables
    let selectedMajor = "All";
    let selectedHousing = "All";
    let selectedTuition = "All";
    let selectedStudent = null;

    // Initialize Dropdown Lists
    function populateFilters() {
      const majors = ["All", ...new Set(RAW_STUDENT_DATA.map(s => s.major))];
      const housings = ["All", ...new Set(RAW_STUDENT_DATA.map(s => s.housing))];
      const tuitions = ["All", ...new Set(RAW_STUDENT_DATA.map(s => s.tuition))];

      const majorSelect = document.getElementById("majorFilter");
      majorSelect.innerHTML = majors.map(m => `<option value="${m}">${m}</option>`).join("");

      const housingSelect = document.getElementById("housingFilter");
      housingSelect.innerHTML = housings.map(h => `<option value="${h}">${h}</option>`).join("");

      const tuitionSelect = document.getElementById("tuitionFilter");
      tuitionSelect.innerHTML = tuitions.map(t => `<option value="${t}">${t}</option>`).join("");
    }

    // Filter Trigger Handler
    function handleFilterChange() {
      selectedMajor = document.getElementById("majorFilter").value;
      selectedHousing = document.getElementById("housingFilter").value;
      selectedTuition = document.getElementById("tuitionFilter").value;
      
      updateDashboard();
    }

    // Reset Trigger Handler
    function handleResetFilters() {
      selectedMajor = "All";
      selectedHousing = "All";
      selectedTuition = "All";
      selectedStudent = null;

      document.getElementById("majorFilter").value = "All";
      document.getElementById("housingFilter").value = "All";
      document.getElementById("tuitionFilter").value = "All";

      updateDashboard();
    }

    // Select Student Click Handler
    function handleSelectStudent(studentId) {
      selectedStudent = RAW_STUDENT_DATA.find(s => s.studentId === studentId) || null;
      renderTable();
      renderSidebar();
    }

    // Comprehensive State & View Redraw engine
    function updateDashboard() {
      // 1. Get filtered cohort
      const filteredData = RAW_STUDENT_DATA.filter(student => {
        const matchMajor = selectedMajor === "All" || student.major === selectedMajor;
        const matchHousing = selectedHousing === "All" || student.housing === selectedHousing;
        const matchTuition = selectedTuition === "All" || student.tuition === selectedTuition;
        return matchMajor && matchHousing && matchTuition;
      });

      // Maintain selection state if filtered out
      if (selectedStudent && !filteredData.some(s => s.studentId === selectedStudent.studentId)) {
        selectedStudent = null;
      }

      // Toggle Clear Filters Button
      const showClearBtn = selectedMajor !== "All" || selectedHousing !== "All" || selectedTuition !== "All";
      document.getElementById("clearFiltersBtn").style.display = showClearBtn ? "flex" : "none";

      // Toggle Empty State / Table Visibility
      if (filteredData.length === 0) {
        document.getElementById("tableWrapper").style.display = "none";
        document.getElementById("emptyState").style.display = "block";
      } else {
        document.getElementById("tableWrapper").style.display = "block";
        document.getElementById("emptyState").style.display = "none";
      }

      // Compute statistics
      let avgGpa = 0;
      let avgAttendance = 0;
      let avgStudyHours = 0;
      let atRiskCount = 0;

      if (filteredData.length > 0) {
        const sumGpa = filteredData.reduce((acc, curr) => acc + curr.gpa, 0);
        const sumAttendance = filteredData.reduce((acc, curr) => acc + curr.attendance, 0);
        const sumStudyHours = filteredData.reduce((acc, curr) => acc + curr.studyHours, 0);
        
        avgGpa = (sumGpa / filteredData.length).toFixed(2);
        avgAttendance = (sumAttendance / filteredData.length).toFixed(1);
        avgStudyHours = (sumStudyHours / filteredData.length).toFixed(1);
        atRiskCount = filteredData.filter(s => s.gpa < 2.5 || s.attendance < 75).length;
      }

      // Update KPI Elements
      document.getElementById("kpiFilteredCohort").textContent = filteredData.length;
      document.getElementById("kpiAvgGpa").textContent = avgGpa;
      document.getElementById("kpiAvgAttendance").textContent = `${avgAttendance}%`;
      
      const kpiAtRiskNode = document.getElementById("kpiAtRisk");
      const kpiAtRiskIconWrapper = document.getElementById("kpiAtRiskIconWrapper");
      kpiAtRiskNode.textContent = atRiskCount;
      if (atRiskCount > 0) {
        kpiAtRiskNode.className = "text-2xl md:text-3xl font-black mt-1 text-rose-400";
        kpiAtRiskIconWrapper.className = "p-3 rounded-lg bg-rose-500/10 text-rose-400";
      } else {
        kpiAtRiskNode.className = "text-2xl md:text-3xl font-black mt-1 text-slate-400";
        kpiAtRiskIconWrapper.className = "p-3 rounded-lg bg-slate-700/20 text-slate-500";
      }

      // Update Cohort Badge on Table Title
      document.getElementById("cohortCountBadge").textContent = `(${filteredData.length} records)`;

      // Draw Dashboard Visualizations
      renderScatterPlot(filteredData);
      renderDistribution(filteredData);
      renderTable(filteredData);
      renderSidebar();
    }

    // Render Scatter Plot Points
    function renderScatterPlot(filteredData) {
      const container = document.getElementById("scatterPoints");
      container.innerHTML = "";

      filteredData.forEach(student => {
        // Study hours max 25, GPA max 4.0
        const xPercent = (student.studyHours / 25) * 100;
        const yPercent = 100 - (student.gpa / 4.0) * 100;

        let dotColorClass = "bg-rose-500";
        if (student.gpa >= 3.5) {
          dotColorClass = "bg-emerald-400";
        } else if (student.gpa >= 2.5) {
          dotColorClass = "bg-indigo-400";
        }

        const pointNode = document.createElement("div");
        pointNode.className = "absolute group cursor-pointer transform -translate-x-1/2 translate-y-1/2 z-10";
        pointNode.style.left = `${xPercent}%`;
        pointNode.style.top = `${yPercent}%`;
        pointNode.onclick = () => handleSelectStudent(student.studentId);

        pointNode.innerHTML = `
          <!-- Dot element -->
          <div class="w-3.5 h-3.5 rounded-full border-2 border-slate-900 shadow-md transition-all duration-150 group-hover:scale-150 ${dotColorClass}"></div>
          
          <!-- Tooltip element on hover -->
          <div class="hidden group-hover:flex absolute bottom-full left-1/2 -translate-x-1/2 mb-2 bg-slate-950 text-white text-[10px] font-bold p-2.5 rounded-lg border border-slate-700 shadow-2xl flex-col min-w-[120px] pointer-events-none z-50">
            <span class="text-indigo-400 font-black">${student.studentId}</span>
            <span>GPA: ${student.gpa}</span>
            <span>Study Hours: ${student.studyHours}h</span>
          </div>
        `;

        container.appendChild(pointNode);
      });
    }

    // Render Major Bar Distribution List
    function renderDistribution(filteredData) {
      const container = document.getElementById("majorDistributionList");
      container.innerHTML = "";

      const distinctMajors = [...new Set(RAW_STUDENT_DATA.map(s => s.major))];

      distinctMajors.forEach(major => {
        const totalInMajor = RAW_STUDENT_DATA.filter(s => s.major === major).length;
        const filteredInMajor = filteredData.filter(s => s.major === major).length;
        const percentageFilled = (filteredInMajor / 10) * 100; // max dataset length is 10

        const distributionItem = document.createElement("div");
        distributionItem.className = "group";
        distributionItem.innerHTML = `
          <div class="flex justify-between text-xs mb-1.5">
            <span class="font-semibold text-slate-300 group-hover:text-indigo-400 transition-colors">${major}</span>
            <span class="text-slate-400 font-mono">
              ${filteredInMajor} <span class="text-slate-600">/ ${totalInMajor} total</span>
            </span>
          </div>
          <div class="w-full bg-slate-900 rounded-full h-3.5 border border-slate-800/80 overflow-hidden relative">
            <div 
              class="h-full bg-gradient-to-r from-indigo-500 to-purple-500 rounded-full transition-all duration-300"
              style="width: ${percentageFilled}%"
            ></div>
          </div>
        `;

        container.appendChild(distributionItem);
      });
    }

    // Render main Student Ledger Directory
    function renderTable(filteredData) {
      const currentFiltered = filteredData || RAW_STUDENT_DATA.filter(student => {
        const matchMajor = selectedMajor === "All" || student.major === selectedMajor;
        const matchHousing = selectedHousing === "All" || student.housing === selectedHousing;
        const matchTuition = selectedTuition === "All" || student.tuition === selectedTuition;
        return matchMajor && matchHousing && matchTuition;
      });

      const tableBody = document.getElementById("directoryTableBody");
      tableBody.innerHTML = "";

      currentFiltered.forEach(student => {
        const isSelected = selectedStudent && selectedStudent.studentId === student.studentId;
        const rowClass = isSelected 
          ? "text-xs hover:bg-slate-800/40 transition duration-150 cursor-pointer bg-indigo-600/10 border-l-4 border-indigo-500" 
          : "text-xs hover:bg-slate-800/40 transition duration-150 cursor-pointer";

        let gpaColorClass = "text-rose-400 bg-rose-500/10";
        if (student.gpa >= 3.5) {
          gpaColorClass = "text-emerald-400 bg-emerald-500/10";
        } else if (student.gpa >= 2.5) {
          gpaColorClass = "text-indigo-400 bg-indigo-500/10";
        }

        let statusClass = "bg-rose-500/10 text-rose-400 border border-rose-500/20";
        if (student.tuition === 'Paid') {
          statusClass = "bg-emerald-500/10 text-emerald-400 border border-emerald-500/20";
        } else if (student.tuition === 'Pending') {
          statusClass = "bg-amber-500/10 text-amber-400 border border-amber-500/20";
        }

        const tableRow = document.createElement("tr");
        tableRow.className = rowClass;
        tableRow.onclick = () => handleSelectStudent(student.studentId);
        tableRow.innerHTML = `
          <td class="py-4 pl-3 font-mono font-bold text-white">${student.studentId}</td>
          <td class="py-4 text-slate-300 font-medium">${student.major}</td>
          <td class="py-4 text-center">
            <span class="px-2 py-0.5 rounded font-bold font-mono ${gpaColorClass}">
              ${student.gpa.toFixed(2)}
            </span>
          </td>
          <td class="py-4 text-center text-slate-300 font-mono">${student.attendance}%</td>
          <td class="py-4 text-center text-slate-300 font-mono">${student.studyHours}h</td>
          <td class="py-4">
            <span class="text-[10px] px-2 py-0.5 rounded-full font-semibold uppercase tracking-wider ${statusClass}">
              ${student.tuition}
            </span>
          </td>
          <td class="py-4 pr-3 text-right">
            <button class="text-slate-500 hover:text-indigo-400 p-1 rounded hover:bg-slate-800 transition">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 animate-pulse-short" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" strokeLinejoin="round" strokeWidth="2" d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
              </svg>
            </button>
          </td>
        `;

        tableBody.appendChild(tableRow);
      });
    }

    // Render Side Panel Profile view
    function renderSidebar() {
      const container = document.getElementById("profileAnalyzerContainer");
      
      if (!selectedStudent) {
        container.innerHTML = `
          <div class="text-center py-12 text-slate-500">
            <svg xmlns="http://www.w3.org/2000/svg" class="mx-auto h-12 w-12 text-slate-700 mb-3" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path strokeLinecap="round" strokeLinejoin="round" strokeWidth="2" d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
            </svg>
            <p class="text-xs">No student selected.</p>
            <p class="text-[11px] text-slate-600 mt-1">Select any row from the student ledger directory to analyze detailed performance vectors.</p>
          </div>
        `;
        return;
      }

      let badgeColorClass = "bg-rose-500/15 text-rose-400";
      let performanceLabel = "At-Risk";
      if (selectedStudent.gpa >= 3.5) {
        badgeColorClass = "bg-emerald-500/15 text-emerald-400";
        performanceLabel = "Excellent";
      } else if (selectedStudent.gpa >= 2.5) {
        badgeColorClass = "bg-indigo-500/15 text-indigo-400";
        performanceLabel = "Good";
      }

      let tuitionBadgeClass = "bg-rose-500/10 text-rose-400";
      if (selectedStudent.tuition === 'Paid') {
        tuitionBadgeClass = "bg-emerald-500/10 text-emerald-400";
      } else if (selectedStudent.tuition === 'Pending') {
        tuitionBadgeClass = "bg-amber-500/10 text-amber-400";
      }

      let recommendationText = "Outstanding status. The student meets all engagement expectations and satisfies required prerequisites.";
      if (selectedStudent.gpa < 2.5) {
        recommendationText = "Academic alert triggered. Recommend scheduling a 1-on-1 advisor review session focusing on self-study hours and class attendance.";
      }

      container.innerHTML = `
        <div class="space-y-6">
          
          <!-- Profile Card Header -->
          <div class="bg-slate-900/60 p-4 rounded-xl border border-slate-850 text-center relative overflow-hidden">
            <div class="absolute top-0 right-0 p-2 text-slate-500 font-mono text-[9px]">
              ${selectedStudent.housing}
            </div>
            <div class="w-14 h-14 bg-indigo-600/20 text-indigo-400 rounded-full flex items-center justify-center mx-auto mb-3 font-mono font-bold text-lg border border-indigo-500/30">
              ${selectedStudent.studentId.slice(3)}
            </div>
            <h4 class="text-md font-black text-white">${selectedStudent.studentId}</h4>
            <p class="text-xs text-slate-400 mt-1 font-semibold">${selectedStudent.major}</p>
          </div>

          <!-- Engagement vs Performance Stats -->
          <div class="space-y-4">
            <h5 class="text-[10px] uppercase tracking-wider font-bold text-slate-400 border-b border-slate-800 pb-1">
              Performance Dimensions
            </h5>

            <!-- Grade Performance -->
            <div class="flex justify-between items-center text-xs">
              <span class="text-slate-400">Grade Point Average</span>
              <div class="flex items-center gap-2">
                <span class="font-mono font-bold text-white">${selectedStudent.gpa.toFixed(2)}</span>
                <span class="text-[10px] px-1.5 py-0.5 rounded ${badgeColorClass}">
                  ${performanceLabel}
                </span>
              </div>
            </div>

            <!-- Attendance -->
            <div class="flex justify-between items-center text-xs">
              <span class="text-slate-400">Classroom Attendance</span>
              <div class="flex items-center gap-2">
                <span class="font-mono font-bold text-white">${selectedStudent.attendance}%</span>
                <span class="text-[10px] text-indigo-400 font-semibold">Active</span>
              </div>
            </div>

            <!-- Weekly Study Hours -->
            <div class="flex justify-between items-center text-xs">
              <span class="text-slate-400">Weekly Study Commits</span>
              <span class="font-mono font-bold text-white">${selectedStudent.studyHours} hours</span>
            </div>

            <!-- Logins & Visits -->
            <div class="grid grid-cols-2 gap-2 bg-slate-900/40 p-3 rounded-lg border border-slate-800 text-center">
              <div>
                <span class="block text-[10px] text-slate-400">LMS Logins / Wk</span>
                <span class="block text-sm font-bold font-mono text-white mt-0.5">${selectedStudent.lmsLogins}</span>
              </div>
              <div class="border-l border-slate-800">
                <span class="block text-[10px] text-slate-400">Library Visits / Mo</span>
                <span class="block text-sm font-bold font-mono text-white mt-0.5">${selectedStudent.libraryVisits}</span>
              </div>
            </div>
          </div>

          <!-- Financial Standings -->
          <div class="space-y-2">
            <h5 class="text-[10px] uppercase tracking-wider font-bold text-slate-400 border-b border-slate-800 pb-1">
              Administrative Standings
            </h5>
            <div class="flex justify-between items-center text-xs">
              <span class="text-slate-400">Tuition Payment Status</span>
              <span class="px-2 py-0.5 rounded font-semibold text-[10px] uppercase ${tuitionBadgeClass}">
                ${selectedStudent.tuition}
              </span>
            </div>
          </div>

          <!-- Action/Intervention Recommendation -->
          <div class="bg-indigo-900/10 border border-indigo-500/20 p-3.5 rounded-lg text-xs">
            <p class="font-semibold text-indigo-400">Intervention Notes:</p>
            <p class="text-slate-400 mt-1 text-[11px] leading-relaxed">
              ${recommendationText}
            </p>
          </div>

        </div>
      `;
    }

    // App Initializer Block
    window.onload = function() {
      populateFilters();
      updateDashboard();
    };
  </script>
</body>
</html>
