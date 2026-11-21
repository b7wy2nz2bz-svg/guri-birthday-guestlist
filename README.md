DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="theme-color" content="#090909">
<title>GURI — Birthday RSVP</title>
<style>
  :root { color-scheme: dark; --bg:#090909; --panel:#111; --line:#292929; --muted:#9b9b9b; --gold:#c8a96b; --white:#f4f1eb; }
  * { box-sizing:border-box; }
  body { margin:0; min-height:100vh; background:radial-gradient(ellipse at 50% -10%, #292218 0, #111 32%, var(--bg) 72%); color:var(--white); font-family:Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif; }
  .wrap { width:min(100% - 32px, 560px); margin:0 auto; padding:44px 0 52px; }
  .eyebrow { color:var(--gold); letter-spacing:.32em; text-transform:uppercase; font-size:10px; text-align:center; }
  h1 { margin:13px 0 3px; text-align:center; font-size:clamp(56px, 16vw, 88px); line-height:.95; letter-spacing:.09em; font-weight:800; }
  .sub { text-align:center; color:#c8c2b7; letter-spacing:.22em; font-size:11px; text-transform:uppercase; margin:13px 0 25px; }
  .rule { width:54px; height:1px; background:var(--gold); margin:0 auto 25px; }
  .event { text-align:center; margin-bottom:27px; }
  .event strong { display:block; font-size:17px; letter-spacing:.12em; font-weight:600; }
  .event span { display:block; margin-top:7px; color:var(--muted); font-size:12px; letter-spacing:.1em; }
  .card { background:rgba(17,17,17,.92); border:1px solid #29251f; border-radius:18px; padding:24px 20px; box-shadow:0 22px 70px #0008; }
  .card h2 { margin:0 0 5px; font-size:20px; font-weight:600; }
  .hint { color:var(--muted); font-size:12px; margin:0 0 22px; }
  label, .field-title { display:block; color:#d9d4ca; font-size:11px; letter-spacing:.12em; text-transform:uppercase; margin:0 0 8px; }
  input, textarea { width:100%; border:1px solid var(--line); background:#0b0b0b; color:var(--white); border-radius:10px; padding:14px 13px; font:inherit; font-size:14px; outline:none; }
  input:focus, textarea:focus { border-color:var(--gold); }
  .field { margin-bottom:17px; }
  .choices { display:grid; grid-template-columns:repeat(3,1fr); gap:8px; }
  .choice input { position:absolute; opacity:0; pointer-events:none; }
  .choice label { display:flex; align-items:center; justify-content:center; min-height:48px; margin:0; border:1px solid var(--line); border-radius:10px; color:#c9c4ba; font-size:12px; letter-spacing:.08em; cursor:pointer; transition:.18s; }
  .choice input:checked + label { border-color:var(--gold); color:var(--gold); background:#c8a96b12; }
  .toggle-row { display:flex; align-items:center; justify-content:space-between; gap:12px; padding:12px 0 4px; }
  .toggle-row label { margin:0; font-size:12px; letter-spacing:.08em; }
  .toggle-row input { width:18px; height:18px; accent-color:var(--gold); }
  .hidden { display:none; }
  button { width:100%; border:0; border-radius:10px; background:var(--gold); color:#111; padding:16px; margin-top:8px; font-size:12px; font-weight:800; letter-spacing:.17em; cursor:pointer; }
  button:hover { background:#ddc18a; }
  .fine { color:#777; font-size:10px; line-height:1.6; text-align:center; margin:15px 5px 0; }
  footer { text-align:center; color:#65615a; font-size:10px; letter-spacing:.2em; margin-top:24px; }
  @media (max-width:380px) { .card { padding:20px 15px; } .choices { gap:5px; } .choice label { font-size:10px; } }
</style>
</head>
<body>
<main class="wrap">
  <div class="eyebrow">You’re invited</div>
  <h1>GURI</h1>
  <div class="sub">Birthday Celebration</div>
  <div class="rule"></div>
  <div class="event">
    <strong>TUESDAY · 24 NOVEMBER</strong>
    <span>10 PM ONWARDS · DELHI</span>
  </div>

  <section class="card">
    <h2>Save your spot.</h2>
    <p class="hint">Drop your details and confirm where you’ll be joining.</p>
    <form id="rsvpForm">
      <div class="field">
        <label for="name">Full name *</label>
        <input id="name" name="name" autocomplete="name" placeholder="Your name" required>
      </div>
      <div class="field">
        <label for="phone">Your WhatsApp / contact number *</label>
        <input id="phone" name="phone" type="tel" autocomplete="tel" placeholder="+91 00000 00000" required>
      </div>
      <div class="field">
        <span class="field-title">Where are you joining? *</span>
        <div class="choices">
          <div class="choice"><input type="radio" id="auro" name="venue" value="AURO" required><label for="auro">AURO</label></div>
          <div class="choice"><input type="radio" id="bulach" name="venue" value="BÜLACH"><label for="bulach">BÜLACH</label></div>
          <div class="choice"><input type="radio" id="both" name="venue" value="BOTH"><label for="both">BOTH</label></div>
        </div>
      </div>
      <div class="field">
        <div class="toggle-row">
          <label for="plusOne">Bringing a plus-one?</label>
          <input id="plusOne" type="checkbox">
        </div>
      </div>
      <div class="field hidden" id="plusOneDetails">
        <label for="guestName">Plus-one name</label>
        <input id="guestName" placeholder="Their full name">
      </div>
      <div class="field">
        <label for="notes">Anything I should know? (optional)</label>
        <textarea id="notes" rows="2" placeholder="Arrival time, group details, etc."></textarea>
      </div>
      <button type="submit">CONFIRM RSVP ON WHATSAPP ↗</button>
    </form>
    <p class="fine">Your RSVP opens WhatsApp with your details ready to send to GURI. Your confirmation is complete once you press Send.</p>
  </section>
  <footer>GOOD PEOPLE · GOOD NIGHT · GURI</footer>
</main>
<script>
  const plusOne = document.getElementById('plusOne');
  const plusOneDetails = document.getElementById('plusOneDetails');
  const guestName = document.getElementById('guestName');
  plusOne.addEventListener('change', () => {
    plusOneDetails.classList.toggle('hidden', !plusOne.checked);
    guestName.required = plusOne.checked;
  });
  document.getElementById('rsvpForm').addEventListener('submit', (e) => {
    e.preventDefault();
    const name = document.getElementById('name').value.trim();
    const phone = document.getElementById('phone').value.trim();
    const venue = document.querySelector('input[name="venue"]:checked')?.value;
    if (!name || !phone || !venue) return;
    const withPlusOne = plusOne.checked;
    const message = [
      'GURI BIRTHDAY RSVP',
      '',
      `Name: ${name}`,
      `Contact: ${phone}`,
      `Joining: ${venue}`,
      `Plus-one: ${withPlusOne ? 'Yes' : 'No'}`,
      ...(withPlusOne ? [`Plus-one name: ${guestName.value.trim()}`] : []),
      ...(document.getElementById('notes').value.trim() ? [`Note: ${document.getElementById('notes').value.trim()}`] : [])
    ].join('\n');
    window.location.href = `https://wa.me/919599155903?text=${encodeURIComponent(message)}`;
  });
</script>
</body>
</html>