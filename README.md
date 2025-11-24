<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://fonts.googleapis.com/css2?family=Crimson+Text:wght@400;600;700&amp;family=Inter:wght@300;400;600;700&amp;display=swap" rel="stylesheet">
  <script src="/_sdk/element_sdk.js"></script>
  <style>
        body {
            box-sizing: border-box;
            margin: 0;
            padding: 0;
            font-family: 'Inter', sans-serif;
            background: #e8f4e8;
            color: #1a4d2e;
            overflow-x: hidden;
        }

        * {
            box-sizing: border-box;
        }

        .sidebar {
            position: fixed;
            left: 0;
            top: 0;
            height: 100%;
            width: 280px;
            background: linear-gradient(180deg, #1a4d2e 0%, #2d6a4f 100%);
            padding: 40px 20px;
            z-index: 100;
            box-shadow: 4px 0 20px rgba(0,0,0,0.1);
        }

        .profile-section {
            text-align: center;
            margin-bottom: 40px;
            padding-bottom: 30px;
            border-bottom: 2px solid rgba(255,255,255,0.2);
        }

        .profile-photo {
            width: 180px;
            height: 180px;
            border-radius: 50%;
            background: linear-gradient(135deg, #52b788 0%, #40916c 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 64px;
            color: white;
            font-weight: 700;
            margin: 0 auto 20px;
            border: 5px solid rgba(255,255,255,0.3);
            box-shadow: 0 10px 30px rgba(0,0,0,0.25);
            position: relative;
            overflow: hidden;
            animation: subtlePulse 3s ease-in-out infinite;
        }

        .profile-photo::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.2), transparent);
            animation: shimmer 4s infinite;
        }

        @keyframes shimmer {
            0% { transform: translateX(-100%) translateY(-100%) rotate(45deg); }
            100% { transform: translateX(100%) translateY(100%) rotate(45deg); }
        }

        @keyframes subtlePulse {
            0%, 100% { box-shadow: 0 8px 24px rgba(0,0,0,0.2); }
            50% { box-shadow: 0 8px 32px rgba(82,183,136,0.4), 0 0 20px rgba(82,183,136,0.2); }
        }

        .profile-photo img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 50%;
        }

        .photo-upload-input {
            display: none;
        }

        .profile-initials {
            font-size: 48px;
            color: white;
            font-weight: 700;
        }

        .profile-name {
            font-family: 'Crimson Text', serif;
            font-size: 40px;
            font-weight: 700;
            color: white;
            margin: 0 0 8px 0;
            line-height: 1.3;
        }

        .profile-title {
            font-size: 13px;
            color: rgba(255,255,255,0.85);
            line-height: 1.4;
        }

        .nav-menu {
            list-style: none;
            padding: 0;
            margin: 0;
        }

        .nav-item {
            margin-bottom: 8px;
        }

        .nav-link {
            display: block;
            padding: 14px 20px;
            color: rgba(255,255,255,0.85);
            text-decoration: none;
            border-radius: 8px;
            transition: all 0.3s ease;
            font-weight: 500;
            font-size: 15px;
            cursor: pointer;
            position: relative;
        }

        .nav-link::before {
            content: '';
            position: absolute;
            left: 0;
            top: 50%;
            transform: translateY(-50%);
            width: 3px;
            height: 0;
            background: linear-gradient(180deg, #95d5b2, #52b788);
            border-radius: 0 3px 3px 0;
            transition: height 0.3s ease;
        }

        .nav-link:hover {
            background: rgba(255,255,255,0.15);
            color: white;
            transform: translateX(5px);
            box-shadow: 0 4px 12px rgba(0,0,0,0.1);
        }

        .nav-link:hover::before {
            height: 60%;
        }

        .nav-link.active {
            background: rgba(255,255,255,0.25);
            color: white;
            font-weight: 600;
            box-shadow: 0 4px 16px rgba(255,255,255,0.1);
        }

        .nav-link.active::before {
            height: 80%;
        }

        .main-content {
            margin-left: 280px;
            padding: 50px;
            min-height: 100%;
        }

        .content-section {
            background: white;
            border-radius: 16px;
            padding: 50px;
            box-shadow: 0 4px 20px rgba(26,77,46,0.08);
            margin-bottom: 30px;
            opacity: 0;
            transform: translateY(30px);
            transition: opacity 0.6s ease, transform 0.6s ease, box-shadow 0.3s ease;
            display: none;
            position: relative;
            overflow: hidden;
        }

        .content-section::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(82,183,136,0.05), transparent);
            animation: cardShimmer 8s infinite;
        }

        .content-section.active {
            display: block;
            animation: fadeInUp 0.6s ease forwards;
        }

        @keyframes fadeInUp {
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        @keyframes cardShimmer {
            0% { left: -100%; }
            50%, 100% { left: 100%; }
        }

        .section-header {
            font-family: 'Crimson Text', serif;
            font-size: 36px;
            color: #1a4d2e;
            margin: 0 0 30px 0;
            padding-bottom: 15px;
            border-bottom: 3px solid #52b788;
            font-weight: 700;
            position: relative;
            animation: headerGlow 4s ease-in-out infinite;
        }

        .section-header::after {
            content: '';
            position: absolute;
            bottom: -3px;
            left: 0;
            width: 0%;
            height: 3px;
            background: linear-gradient(90deg, #52b788, #95d5b2, #52b788);
            animation: borderShine 3s ease-in-out infinite;
        }

        @keyframes headerGlow {
            0%, 100% { text-shadow: 0 0 5px rgba(82,183,136,0); }
            50% { text-shadow: 0 0 10px rgba(82,183,136,0.3); }
        }

        @keyframes borderShine {
            0%, 100% { width: 0%; left: 0; }
            50% { width: 100%; left: 0; }
        }

        .contact-bar {
            display: flex;
            flex-wrap: wrap;
            gap: 30px;
            padding: 25px;
            background: linear-gradient(135deg, #f1faee 0%, #e8f4e8 100%);
            border-radius: 12px;
            margin-bottom: 35px;
            border-left: 4px solid #40916c;
        }

        .contact-item {
            display: flex;
            align-items: center;
            gap: 10px;
            font-size: 15px;
            color: #1a4d2e;
        }

        .contact-icon {
            width: 20px;
            height: 20px;
            fill: #40916c;
        }

        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .info-card {
            padding: 20px;
            background: #f8fdf8;
            border-radius: 10px;
            border-left: 3px solid #52b788;
        }

        .info-label {
            font-weight: 700;
            color: #2d6a4f;
            font-size: 14px;
            margin-bottom: 6px;
        }

        .info-value {
            color: #1a4d2e;
            font-size: 15px;
        }

        .objective-text {
            font-size: 17px;
            line-height: 1.8;
            color: #1a4d2e;
            padding: 30px;
            background: linear-gradient(135deg, #f1faee 0%, #e8f4e8 100%);
            border-radius: 12px;
            border-left: 4px solid #40916c;
            font-style: italic;
        }

        .education-timeline {
            position: relative;
            padding-left: 40px;
            margin-top: 30px;
        }

        .education-timeline::before {
            content: '';
            position: absolute;
            left: 0;
            top: 0;
            bottom: 0;
            width: 3px;
            background: linear-gradient(180deg, #52b788 0%, #95d5b2 100%);
        }

        .education-item {
            position: relative;
            margin-bottom: 35px;
            padding: 25px;
            background: #f8fdf8;
            border-radius: 12px;
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }

        .education-item:hover {
            transform: translateX(8px);
            box-shadow: 0 6px 20px rgba(26,77,46,0.1);
        }

        .education-item::before {
            content: '';
            position: absolute;
            left: -48px;
            top: 30px;
            width: 16px;
            height: 16px;
            background: #40916c;
            border-radius: 50%;
            border: 3px solid #e8f4e8;
            box-shadow: 0 0 0 0 rgba(82,183,136,0.5);
            animation: timelinePulse 2s infinite;
        }

        @keyframes timelinePulse {
            0%, 100% { box-shadow: 0 0 0 0 rgba(82,183,136,0.5); }
            50% { box-shadow: 0 0 0 8px rgba(82,183,136,0); }
        }

        .education-title {
            font-family: 'Crimson Text', serif;
            font-size: 22px;
            font-weight: 700;
            color: #1a4d2e;
            margin: 0 0 8px 0;
        }

        .education-subtitle {
            font-size: 16px;
            color: #2d6a4f;
            margin-bottom: 12px;
            font-weight: 600;
        }

        .education-year {
            display: inline-block;
            padding: 6px 14px;
            background: #d8f3dc;
            color: #2d6a4f;
            border-radius: 20px;
            font-size: 13px;
            font-weight: 600;
            margin-bottom: 15px;
        }

        .education-details {
            list-style: none;
            padding: 0;
            margin: 15px 0 0 0;
        }

        .education-details li {
            padding: 8px 0 8px 28px;
            position: relative;
            color: #1a4d2e;
            font-size: 15px;
            line-height: 1.6;
        }

        .education-details li::before {
            content: '•';
            position: absolute;
            left: 0;
            color: #40916c;
            font-weight: 700;
            font-size: 16px;
        }

        .awards-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
            gap: 20px;
            margin-top: 25px;
        }

        .award-card {
            padding: 25px;
            background: linear-gradient(135deg, #ffffff 0%, #f8fdf8 100%);
            border-radius: 12px;
            border: 2px solid #d8f3dc;
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .award-card::before {
            content: '';
            position: absolute;
            top: -50%;
            right: -50%;
            width: 100%;
            height: 100%;
            background: radial-gradient(circle, rgba(82,183,136,0.1) 0%, transparent 70%);
            animation: iconGlow 3s ease-in-out infinite;
        }

        .award-card:hover {
            transform: translateY(-5px);
            border-color: #52b788;
            box-shadow: 0 8px 20px rgba(26,77,46,0.12), 0 0 30px rgba(82,183,136,0.1);
        }

        .award-icon {
            font-size: 36px;
            margin-bottom: 12px;
            display: inline-block;
            animation: iconFloat 3s ease-in-out infinite;
            position: relative;
            z-index: 1;
        }

        @keyframes iconGlow {
            0%, 100% { transform: scale(1); opacity: 0.3; }
            50% { transform: scale(1.5); opacity: 0.6; }
        }

        @keyframes iconFloat {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-5px); }
        }

        .award-text {
            color: #1a4d2e;
            font-size: 15px;
            line-height: 1.6;
        }

        .activities-list {
            list-style: none;
            padding: 0;
            margin: 25px 0 0 0;
        }

        .activities-list li {
            padding: 18px 25px 18px 55px;
            margin-bottom: 15px;
            background: #f8fdf8;
            border-radius: 10px;
            position: relative;
            color: #1a4d2e;
            font-size: 15px;
            line-height: 1.6;
            transition: all 0.3s ease;
        }

        .activities-list li:hover {
            background: #d8f3dc;
            transform: translateX(5px);
        }

        .activities-list li::before {
            content: '●';
            position: absolute;
            left: 25px;
            color: #40916c;
            font-size: 24px;
            line-height: 1;
        }

        .skills-grid {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            margin-top: 25px;
        }

        .skill-badge {
            padding: 12px 24px;
            background: linear-gradient(135deg, #52b788 0%, #40916c 100%);
            color: white;
            border-radius: 25px;
            font-size: 14px;
            font-weight: 600;
            transition: all 0.3s ease;
            cursor: default;
            position: relative;
            overflow: hidden;
        }

        .skill-badge::before {
            content: '';
            position: absolute;
            top: -50%;
            left: -50%;
            width: 200%;
            height: 200%;
            background: linear-gradient(45deg, transparent, rgba(255,255,255,0.3), transparent);
            transform: translateX(-100%) translateY(-100%) rotate(45deg);
            transition: transform 0.6s ease;
        }

        .skill-badge:hover {
            transform: translateY(-3px);
            box-shadow: 0 6px 16px rgba(64,145,108,0.3), 0 0 20px rgba(82,183,136,0.2);
        }

        .skill-badge:hover::before {
            transform: translateX(100%) translateY(100%) rotate(45deg);
        }

        .reference-card {
            background: linear-gradient(135deg, #2d6a4f 0%, #1a4d2e 100%);
            color: white;
            padding: 35px;
            border-radius: 12px;
            text-align: center;
            margin-top: 25px;
        }

        .reference-name {
            font-family: 'Crimson Text', serif;
            font-size: 26px;
            font-weight: 700;
            margin-bottom: 10px;
        }

        .reference-position {
            font-size: 16px;
            margin-bottom: 5px;
            opacity: 0.95;
        }

        .reference-contact {
            font-size: 15px;
            margin-top: 15px;
            opacity: 0.9;
        }

        @media (max-width: 968px) {
            .sidebar {
                position: relative;
                width: 100%;
                height: auto;
            }

            .main-content {
                margin-left: 0;
                padding: 30px 20px;
            }

            .content-section {
                padding: 30px 25px;
            }

            .section-header {
                font-size: 28px;
            }

            .contact-bar {
                flex-direction: column;
                gap: 15px;
            }

            .info-grid {
                grid-template-columns: 1fr;
            }

            .awards-grid {
                grid-template-columns: 1fr;
            }
        }
    </style>
  <style>@view-transition { navigation: auto; }</style>
  <script src="/_sdk/data_sdk.js" type="text/javascript"></script>
  <script src="https://cdn.tailwindcss.com" type="text/javascript"></script>
 </head>
 <body>
  <nav class="sidebar">
   <div class="profile-section">
    <div class="profile-photo" id="profilePhoto"><span class="profile-initials" id="profileInitials">AM</span>
    </div>
    <h1 class="profile-name" id="profileName">Alberto Jose C. Mangali</h1>
    <p class="profile-title" id="profileTitle">Financial Management Student</p>
   </div>
   <ul class="nav-menu">
    <li class="nav-item"><a class="nav-link active" data-section="about">About Me</a></li>
    <li class="nav-item"><a class="nav-link" data-section="personal">Personal Information</a></li>
    <li class="nav-item"><a class="nav-link" data-section="objective">Objective</a></li>
    <li class="nav-item"><a class="nav-link" data-section="education">Education</a></li>
    <li class="nav-item"><a class="nav-link" data-section="awards">Awards</a></li>
    <li class="nav-item"><a class="nav-link" data-section="leadership">Leadership</a></li>
    <li class="nav-item"><a class="nav-link" data-section="journalism">Journalism</a></li>
    <li class="nav-item"><a class="nav-link" data-section="skills">Skills</a></li>
    <li class="nav-item"><a class="nav-link" data-section="reference">Reference</a></li>
   </ul>
  </nav>
  <main class="main-content">
   <section id="about" class="content-section active">
    <h2 class="section-header">About Me</h2>
    <div class="contact-bar">
     <div class="contact-item">
      <svg class="contact-icon" viewbox="0 0 24 24"><path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z" />
      </svg><span id="addressText">1036 Adelfa St., Merville Subd., Tanza 1, Navotas City, Metro Manila</span>
     </div>
     <div class="contact-item">
      <svg class="contact-icon" viewbox="0 0 24 24"><path d="M6.62 10.79c1.44 2.83 3.76 5.14 6.59 6.59l2.2-2.2c.27-.27.67-.36 1.02-.24 1.12.37 2.33.57 3.57.57.55 0 1 .45 1 1V20c0 .55-.45 1-1 1-9.39 0-17-7.61-17-17 0-.55.45-1 1-1h3.5c.55 0 1 .45 1 1 0 1.25.2 2.45.57 3.57.11.35.03.74-.25 1.02l-2.2 2.2z" />
      </svg><span id="phoneText">09917759750</span>
     </div>
     <div class="contact-item">
      <svg class="contact-icon" viewbox="0 0 24 24"><path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z" />
      </svg><span id="emailText">mangalialbertojose0@gmail.com</span>
     </div>
    </div>
    <p style="font-size: 17px; line-height: 1.8; color: #1a4d2e; margin-bottom: 30px;">A dedicated Financial Management college student currently pursuing a Bachelor of Science in Business Administration, with a proven track record of academic excellence from elementary through college. Recognized as Class Valedictorian and recipient of the Philippine Senate Gold Medal for Academic Excellence in Senior High School, I bring strong analytical skills, leadership experience, and a commitment to continuous growth and learning.</p>
    <div style="padding: 25px; background: linear-gradient(135deg, #f1faee 0%, #e8f4e8 100%); border-radius: 12px; border-left: 4px solid #40916c; margin-bottom: 25px;">
     <h3 style="font-family: 'Crimson Text', serif; font-size: 22px; font-weight: 700; color: #1a4d2e; margin: 0 0 15px 0;">Career Aspirations</h3>
     <p style="font-size: 16px; line-height: 1.8; color: #1a4d2e; margin: 0;">I'm majoring in Financial Management because I see myself thriving in the finance world—whether that's working in a bank, becoming a financial advisor, stepping into the role of a chief financial officer, or even teaching finance someday as a professor. I'm excited to build the foundation for that future here in college.</p>
    </div>
    <div style="padding: 25px; background: #f8fdf8; border-radius: 12px; border-left: 4px solid #52b788; margin-bottom: 25px;">
     <h3 style="font-family: 'Crimson Text', serif; font-size: 22px; font-weight: 700; color: #1a4d2e; margin: 0 0 15px 0;">Hobbies &amp; Interests</h3>
     <p style="font-size: 16px; line-height: 1.8; color: #1a4d2e; margin: 0;">Outside of academics, I enjoy watching short clips on TikTok and bingeing series online, especially K-dramas and fantasy shows. I also like reading from time to time, but I'm more into writing—it's how I express myself best.</p>
    </div>
    <div style="padding: 30px; background: linear-gradient(135deg, #2d6a4f 0%, #1a4d2e 100%); border-radius: 12px; text-align: center;">
     <h3 style="font-family: 'Crimson Text', serif; font-size: 20px; font-weight: 700; color: white; margin: 0 0 15px 0;">Favorite Quote</h3>
     <p style="font-size: 18px; line-height: 1.8; color: white; margin: 0 0 10px 0; font-style: italic;">"You must be the change you wish to see in the world."</p>
     <p style="font-size: 15px; color: rgba(255,255,255,0.85); margin: 0;">– Mahatma Gandhi</p>
    </div>
   </section>
   <section id="personal" class="content-section">
    <h2 class="section-header">Personal Information</h2>
    <div class="info-grid">
     <div class="info-card">
      <div class="info-label">
       Date of Birth
      </div>
      <div class="info-value">
       August 26, 2006
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Age
      </div>
      <div class="info-value">
       19
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Place of Birth
      </div>
      <div class="info-value">
       San Jose, Navotas City
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Citizenship
      </div>
      <div class="info-value">
       Filipino
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Religion
      </div>
      <div class="info-value">
       Roman Catholic
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Civil Status
      </div>
      <div class="info-value">
       Single
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Height
      </div>
      <div class="info-value">
       5'3"
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Weight
      </div>
      <div class="info-value">
       44.4 kgs
      </div>
     </div>
     <div class="info-card">
      <div class="info-label">
       Languages
      </div>
      <div class="info-value">
       Filipino, English
      </div>
     </div>
    </div>
   </section>
   <section id="objective" class="content-section">
    <h2 class="section-header">Career Objective</h2>
    <div class="objective-text" id="objectiveText">
     To apply the knowledge and skills I have gained from my education and experiences by contributing effectively to your company's success. I am committed to offering dedication, adaptability, and a strong work ethic, with the goal of becoming a valuable asset while continuously learning and growing in my career.
    </div>
   </section>
   <section id="education" class="content-section">
    <h2 class="section-header">Education</h2>
    <div class="education-timeline">
     <div class="education-item">
      <div class="education-year">
       AY 2024–Present
      </div>
      <div class="education-title">
       Navotas Polytechnic College
      </div>
      <div class="education-subtitle">
       BSBA – Major in Financial Management (Currently Sophomore)
      </div>
      <ul class="education-details">
       <li>Class Representative of Section FM 1C, 2nd Semester, 1st Year</li>
       <li>Freshman Year: Sertipiko ng Pagkilala – Natatanging Kahusayan sa Larangan ng Akademiko (AY 2024–2025)</li>
       <li>Navotas Scholarship Recipient</li>
       <li>Entrance Examination Passer</li>
      </ul>
     </div>
     <div class="education-item">
      <div class="education-year">
       SY 2023–2024
      </div>
      <div class="education-title">
       Tanza National High School
      </div>
      <div class="education-subtitle">
       Senior High School – Accountancy, Business and Management (ABM) Strand, SDO Navotas City
      </div>
      <ul class="education-details">
       <li>Batch 'Sinagtala' Class Valedictorian, With Highest Honors</li>
       <li>Class Vice-President</li>
       <li>Philippine Senate Gold Medal for Academic Excellence Awardee</li>
       <li>Delivered Valedictory Speech: "Mensahe mula sa Kinatawan ng Magsisipagtapos"</li>
      </ul>
     </div>
     <div class="education-item">
      <div class="education-year">
       SY 2019–2022
      </div>
      <div class="education-title">
       Junior High School
      </div>
      <div class="education-subtitle">
       Tanza National High School – SDO Navotas City
      </div>
      <ul class="education-details">
       <li>With High Honors</li>
       <li>Also attended: Malabon National High School – SDO Malabon City (SY 2018–2019)</li>
      </ul>
     </div>
     <div class="education-item">
      <div class="education-year">
       SY 2011–2018
      </div>
      <div class="education-title">
       Elementary
      </div>
      <div class="education-subtitle">
       Malabon Elementary School – SDO Malabon City
      </div>
      <ul class="education-details">
       <li>Consistent Academic Awardee</li>
      </ul>
     </div>
    </div>
   </section>
   <section id="awards" class="content-section">
    <h2 class="section-header">Academic Achievements &amp; Awards</h2>
    <div class="awards-grid">
     <div class="award-card">
      <div class="award-icon">
       🏆
      </div>
      <div class="award-text">
       Consistent Academic Awardee (Elementary to College)
      </div>
     </div>
     <div class="award-card">
      <div class="award-icon">
       ⭐
      </div>
      <div class="award-text">
       Outstanding Performance in Science, Mathematics, Communication Arts, and Work Immersion
      </div>
     </div>
     <div class="award-card">
      <div class="award-icon">
       📜
      </div>
      <div class="award-text">
       Certificate of Academic Excellence – SHS Grade 12 (Highest Honors, SY 2023–2024)
      </div>
     </div>
     <div class="award-card">
      <div class="award-icon">
       📜
      </div>
      <div class="award-text">
       Certificate of Academic Excellence – SHS Grade 11 (High Honors, SY 2022–2023)
      </div>
     </div>
     <div class="award-card">
      <div class="award-icon">
       📜
      </div>
      <div class="award-text">
       Certificate of Academic Excellence – JHS Completion (High Honors, SY 2021–2022)
      </div>
     </div>
     <div class="award-card">
      <div class="award-icon">
       ✍️
      </div>
      <div class="award-text">
       Certificate of Recognition – Journalist of the Year 2023
      </div>
     </div>
    </div>
   </section>
   <section id="leadership" class="content-section">
    <h2 class="section-header">Leadership &amp; Extracurricular Activities</h2>
    <ul class="activities-list">
     <li>Class Representative of Section FM 1C, 2nd Semester, 1st Year – Navotas Polytechnic College</li>
     <li>2024 Philippines–South Korea International Youth Exchange Program – Delegate</li>
     <li>Interact Club of Tanza National High School – Director of Basic Education and Literacy</li>
     <li>The Sparks – Official School Publication (English) – Editor-in-Chief (2 consecutive years)</li>
     <li>Grade 12 – Class Vice-President</li>
     <li>Grade 11 – Class President</li>
    </ul>
   </section>
   <section id="journalism" class="content-section">
    <h2 class="section-header">Journalism &amp; Competitions</h2>
    <ul class="activities-list">
     <li>2024 Division Schools Press Conference – Secondary – News Writing – 5th Placer</li>
     <li>2023 Division Schools Press Conference – Secondary – News Writing – 1st Placer</li>
     <li>2023 Regional Schools Press Conference – Secondary – News Writing – Qualifier</li>
     <li>Journalist of the Year 2023</li>
    </ul>
   </section>
   <section id="skills" class="content-section">
    <h2 class="section-header">Skills</h2>
    <div class="skills-grid"><span class="skill-badge">Financial Accounting</span> <span class="skill-badge">Journal &amp; Ledger Management</span> <span class="skill-badge">Financial Statements</span> <span class="skill-badge">Analytical Thinking</span> <span class="skill-badge">Problem Solving</span> <span class="skill-badge">Written Communication</span> <span class="skill-badge">Oral Communication</span> <span class="skill-badge">Independent Work</span> <span class="skill-badge">Team Collaboration</span> <span class="skill-badge">Organization</span> <span class="skill-badge">Management</span> <span class="skill-badge">Motivation</span> <span class="skill-badge">Determination</span> <span class="skill-badge">Consistency</span>
    </div>
   </section>
   <section id="reference" class="content-section">
    <h2 class="section-header">Character Reference</h2>
    <div class="reference-card">
     <div class="reference-name">
      Dr. Jassele S. Lim
     </div>
     <div class="reference-position">
      Senior High School Teacher and Adviser
     </div>
     <div class="reference-position">
      Tanza National High School – SDO Navotas City
     </div>
     <div class="reference-contact">
      📞 09454121241
     </div>
    </div>
   </section>
  </main>
  <script>
        const defaultConfig = {
            full_name: "Alberto Jose C. Mangali",
            job_title: "Financial Management Student",
            email: "mangalialbertojose0@gmail.com",
            phone: "09917759750",
            address: "1036 Adelfa St., Merville Subd., Tanza 1, Navotas City, Metro Manila",
            objective_text: "To apply the knowledge and skills I have gained from my education and experiences by contributing effectively to your company's success. I am committed to offering dedication, adaptability, and a strong work ethic, with the goal of becoming a valuable asset while continuously learning and growing in my career."
        };

        const navLinks = document.querySelectorAll('.nav-link');
        const sections = document.querySelectorAll('.content-section');
        const profilePhoto = document.getElementById('profilePhoto');
        const profileInitials = document.getElementById('profileInitials');

        // Load permanent profile photo on page load
        function loadPermanentPhoto() {
            const permanentPhotoUrl = 'https://i.postimg.cc/cvPPvRBv/profile.jpg';
            
            const img = document.createElement('img');
            img.src = permanentPhotoUrl;
            img.alt = 'Alberto Jose C. Mangali';
            
            img.onload = function() {
                profileInitials.style.display = 'none';
                profilePhoto.appendChild(img);
            };
            
            img.onerror = function() {
                // If image fails to load, keep showing initials
                profileInitials.style.display = 'flex';
            };
        }

        // Load permanent photo immediately
        loadPermanentPhoto();

        navLinks.forEach(link => {
            link.addEventListener('click', function(e) {
                e.preventDefault();
                const targetSection = this.getAttribute('data-section');
                
                navLinks.forEach(l => l.classList.remove('active'));
                this.classList.add('active');
                
                sections.forEach(section => {
                    section.classList.remove('active');
                });
                
                const target = document.getElementById(targetSection);
                if (target) {
                    target.classList.add('active');
                    if (window.innerWidth > 968) {
                        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
                    }
                }
            });
        });

        async function onConfigChange(config) {
            const fullName = config.full_name || defaultConfig.full_name;
            const jobTitle = config.job_title || defaultConfig.job_title;
            const email = config.email || defaultConfig.email;
            const phone = config.phone || defaultConfig.phone;
            const address = config.address || defaultConfig.address;
            const objectiveText = config.objective_text || defaultConfig.objective_text;

            document.getElementById('profileName').textContent = fullName;
            document.getElementById('profileTitle').textContent = jobTitle;
            document.getElementById('emailText').textContent = email;
            document.getElementById('phoneText').textContent = phone;
            document.getElementById('addressText').textContent = address;
            document.getElementById('objectiveText').textContent = objectiveText;

            const nameParts = fullName.split(' ');
            const initials = nameParts.length >= 2 
                ? (nameParts[0][0] + nameParts[nameParts.length - 1][0]).toUpperCase()
                : fullName.substring(0, 2).toUpperCase();
            
            const profileInitialsElement = document.getElementById('profileInitials');
            if (profileInitialsElement) {
                profileInitialsElement.textContent = initials;
            }
        }

        function mapToCapabilities(config) {
            return {
                recolorables: [],
                borderables: [],
                fontEditable: undefined,
                fontSizeable: undefined
            };
        }

        function mapToEditPanelValues(config) {
            return new Map([
                ["full_name", config.full_name || defaultConfig.full_name],
                ["job_title", config.job_title || defaultConfig.job_title],
                ["email", config.email || defaultConfig.email],
                ["phone", config.phone || defaultConfig.phone],
                ["address", config.address || defaultConfig.address],
                ["objective_text", config.objective_text || defaultConfig.objective_text]
            ]);
        }

        if (window.elementSdk) {
            window.elementSdk.init({
                defaultConfig,
                onConfigChange,
                mapToCapabilities,
                mapToEditPanelValues
            });
        }
    </script>
 <script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'9a36334802359949',t:'MTc2Mzk1ODkzNC4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
