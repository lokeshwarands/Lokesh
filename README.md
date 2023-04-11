# Answer

function getDailySum(inputDict) {
  const outputDict = {
    'Mon': 0,
    'Tue': 0,
    'Wed': 0,
    'Thu': 0,
    'Fri': 0,
    'Sat': 0,
    'Sun': 0
  };

  const inputKeys = Object.keys(inputDict).sort();

  for (let i = 0; i < inputKeys.length; i++) {
    const currKey = inputKeys[i];
    const currValue = inputDict[currKey];

   const day = new Date(currKey).toLocaleString('en-us', { weekday: 'short' });

   outputDict[day] += currValue;

   if (day !== 'Sun' && i < inputKeys.length - 1) {
      const nextKey = inputKeys[i + 1];
      const nextDay = new Date(nextKey).toLocaleString('en-us', { weekday: 'short' });

   if (day !== nextDay) {
        const meanValue = Math.floor((currValue + inputDict[nextKey]) / 2);
        outputDict[nextDay] += meanValue;
      }
    }

   if (day !== 'Mon' && i > 0) {
      const prevKey = inputKeys[i - 1];
      const prevDay = new Date(prevKey).toLocaleString('en-us', { weekday: 'short' });

   if (day !== prevDay) {
        const meanValue = Math.floor((currValue + inputDict[prevKey]) / 2);
        outputDict[prevDay] += meanValue;
      }
    }
  }

  return outputDict;
}
