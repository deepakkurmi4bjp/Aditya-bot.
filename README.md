document.addEventListener("DOMContentLoaded", function () {
  const chatbox = document.getElementById("chatbox");
  const inputBox = document.getElementById("userText");
  const sendButton = document.getElementById("sendBtn");

  const yojnaList = {
    hindi: {
      "प्रधानमंत्री उज्ज्वला योजना": "बीपीएल परिवारों को मुफ्त गैस कनेक्शन प्रदान किया जाता है।",
      "लाडली बहना योजना": "मध्यप्रदेश की महिलाओं को ₹1250 प्रति माह की आर्थिक सहायता।",
      "प्रधानमंत्री किसान सम्मान निधि": "₹6000 वार्षिक सहायता छोटे और सीमांत किसानों को मिलती है।"
    },
    english: {
      "Ujjwala Yojana": "Free LPG connections for BPL families.",
      "Ladli Behna Yojana": "₹1250 monthly support for women in Madhya Pradesh.",
      "PM-KISAN": "₹6000 annual support to small and marginal farmers."
    }
  };

  let currentLang = "hindi";

  function appendMessage(sender, text) {
    const message = document.createElement("div");
    message.innerHTML = `<b>${sender}:</b> ${text}`;
    chatbox.appendChild(message);
    chatbox.scrollTop = chatbox.scrollHeight;
  }

  function processInput() {
    const input = inputBox.value.trim();
    if (!input) return;

    appendMessage("You", input);
    inputBox.value = "";

    let reply = currentLang === "hindi" ? "माफ कीजिए, मुझे वह योजना नहीं मिली।" : "Sorry, I couldn't find that scheme.";

    if (input.toLowerCase().includes("language")) {
      currentLang = currentLang === "hindi" ? "english" : "hindi";
      reply = currentLang === "hindi" ? "भाषा अब हिंदी में है।" : "Language switched to English.";
    } else {
      const yojna = yojnaList[currentLang];
      for (let key in yojna) {
        if (input.toLowerCase().includes(key.toLowerCase())) {
          reply = yojna[key];
          break;
        }
      }
    }

    setTimeout(() => {
      appendMessage("Aditya", reply);
    }, 300);
  }

  sendButton.addEventListener("click", processInput);
  inputBox.addEventListener("keypress", function (e) {
    if (e.key === "Enter") {
      processInput();
    }
  });
});
