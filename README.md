# resumemaker<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Resume Builder</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins&display=swap" rel="stylesheet">
  <style>
    * { font-family: 'Poppins', sans-serif; }
    body { margin: 0; padding: 0; background: #f0f2f5; }
    .container { display: flex; flex-direction: column; align-items: center; padding: 2rem; }
    h1 { margin-bottom: 1rem; }
    form, .resume-preview { background: white; padding: 2rem; border-radius: 10px; width: 100%; max-width: 700px; margin-bottom: 2rem; box-shadow: 0 0 10px rgba(0,0,0,0.1); }
    input, textarea { width: 100%; margin-bottom: 1rem; padding: 0.7rem; border: 1px solid #ccc; border-radius: 5px; }
    label { font-weight: bold; display: block; margin-top: 1rem; }
    #downloadBtn { padding: 0.7rem 1.2rem; background: #007bff; color: white; border: none; border-radius: 5px; cursor: pointer; }
    .resume-box { padding: 1rem; border: 1px solid #ddd; }
  </style>
</head>
<body>
  <div class="container">
    <h1>Resume Builder</h1>
    <form id="resumeForm">
      <label>What is your full name?</label>
      <input type="text" id="name" required />

      <label>Where are you from? (City, State)</label>
      <input type="text" id="location" required />

      <label>What is your email address?</label>
      <input type="email" id="email" required />

      <label>What is your phone number?</label>
      <input type="text" id="phone" required />

      <label>Where did you study your 10th? Year? Marks?</label>
      <textarea id="class10" rows="2" required></textarea>

      <label>Where did you study your 12th? Year? Marks?</label>
      <textarea id="class12" rows="2" required></textarea>

      <label>Your BCA college name, university and expected graduation year?</label>
      <textarea id="bca" rows="2" required></textarea>

      <label>What technical skills do you know or are learning?</label>
      <textarea id="skills" rows="3" required></textarea>

      <label>What languages can you speak or write?</label>
      <textarea id="languages" rows="2" required></textarea>

      <label>What are your areas of interest (e.g., animation, software dev)?</label>
      <textarea id="interests" rows="2"></textarea>

      <button type="submit">Generate Resume</button>
    </form>

    <div class="resume-preview" id="resumePreview" style="display: none">
      <h2>Resume Preview</h2>
      <div class="resume-box" id="resumeContent"></div>
      <button id="downloadBtn">Download PDF</button>
    </div>
  </div>

  <script src="https://cdnjs.cloudflare.com/ajax/libs/html2pdf.js/0.10.1/html2pdf.bundle.min.js"></script>
  <script>
    const form = document.getElementById('resumeForm');
    const resumeContent = document.getElementById('resumeContent');
    const preview = document.getElementById('resumePreview');
    const downloadBtn = document.getElementById('downloadBtn');

    form.addEventListener('submit', function (e) {
      e.preventDefault();

      const name = document.getElementById('name').value;
      const location = document.getElementById('location').value;
      const email = document.getElementById('email').value;
      const phone = document.getElementById('phone').value;
      const class10 = document.getElementById('class10').value;
      const class12 = document.getElementById('class12').value;
      const bca = document.getElementById('bca').value;
      const skills = document.getElementById('skills').value;
      const languages = document.getElementById('languages').value;
      const interests = document.getElementById('interests').value;

      resumeContent.innerHTML = `
        <h2>${name}</h2>
        <p><strong>Location:</strong> ${location}</p>
        <p><strong>Email:</strong> ${email}</p>
        <p><strong>Phone:</strong> ${phone}</p>

        <h3>Career Objective</h3>
        <p>Aspiring software developer and computer science student passionate about learning programming, web development, and creative technologies. Seeking opportunities to grow through hands-on projects and collaborative learning.</p>

        <h3>Education</h3>
        <p><strong>10th:</strong><br>${class10.replace(/\n/g, '<br>')}</p>
        <p><strong>12th:</strong><br>${class12.replace(/\n/g, '<br>')}</p>
        <p><strong>BCA:</strong><br>${bca.replace(/\n/g, '<br>')}</p>

        <h3>Skills</h3>
        <p>${skills.replace(/\n/g, '<br>')}</p>

        <h3>Languages</h3>
        <p>${languages.replace(/\n/g, '<br>')}</p>

        <h3>Interests</h3>
        <p>${interests.replace(/\n/g, '<br>')}</p>

        <h3>Declaration</h3>
        <p>I hereby declare that all the information mentioned above is true to the best of my knowledge.</p>
        <p><strong>${name}</strong></p>
      `;

      preview.style.display = 'block';
    });

    downloadBtn.addEventListener('click', function () {
      html2pdf().from(resumeContent).save("Resume.pdf");
    });
  </script>
</body>
</html>
