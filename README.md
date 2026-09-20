    const CONFIG = {
      gateways: {
        Linkvertise: {
          name: "Linkvertise",
          // 12-Hour Pass (3 Checkpoints) - Paste your Linkvertise links here:
          tier12: [
            "https://linkvertise.com/your-cp1-link-here", // Checkpoint 1 (target: https://shuraminkio.github.io/?step=2&tier=12)
            "https://linkvertise.com/your-cp2-link-here", // Checkpoint 2 (target: https://shuraminkio.github.io/?step=3&tier=12)
            "https://linkvertise.com/your-cp3-link-here"  // Checkpoint 3 (target: https://shuraminkio.github.io/?step=4&tier=12)
          ],
          // 24-Hour Pass (6 Checkpoints) - Paste your 24h Linkvertise links here:
          tier24: [
            "https://linkvertise.com/your-24h-cp1-here",
            "https://linkvertise.com/your-24h-cp2-here",
            "https://linkvertise.com/your-24h-cp3-here",
            "https://linkvertise.com/your-24h-cp4-here",
            "https://linkvertise.com/your-24h-cp5-here",
            "https://linkvertise.com/your-24h-cp6-here"
          ],
          getUrl: function(tierHours, step) {
            const list = (tierHours === 24) ? this.tier24 : this.tier12;
            const idx = step - 1;
            if (list && list[idx] && !list[idx].includes("your-")) {
              return list[idx];
            }
            return `https://linkvertise.com?r=minkio_${tierHours}h_step${step}`;
          }
        },
