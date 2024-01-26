# initial-commit


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace ExoDictionary
{

    public class DictionaryReplacer
    {
        public static string Replace(string input, Dictionary<string, string> dictionary)
        {
            if (string.IsNullOrEmpty(input) || dictionary == null || dictionary.Count == 0)
            {
                return input;
            }

            foreach (var entry in dictionary)
            {
                string key = $"${entry.Key}$";
                if (input.Contains(key))
                {
                    input = input.Replace(key, entry.Value);
                }
            }

            return input;
        }
    }
}


using ExoDictionary;
using Microsoft.VisualStudio.TestTools.UnitTesting;
using System.Collections.Generic;

namespace DictionaryReplacerTests
{
    
        [TestClass]
        public class DictionaryReplacerTests
        {
            [TestMethod]
            public void Replace_WithEmptyStringAndEmptyDictionary_ReturnsEmptyString()
            {
                // Arrange
                string input = "";
                var dictionary = new Dictionary<string, string>();

                // Act
                string result = DictionaryReplacer.Replace(input, dictionary);

                // Assert
                Assert.AreEqual("", result);
            }

            [TestMethod]
            public void Replace_WithSingleKeyAndValueInDictionary_ReturnsReplacedString()
            {
                // Arrange
                string input = "$temp$";
                var dictionary = new Dictionary<string, string> { { "temp", "temporary" } };

                // Act
                string result = DictionaryReplacer.Replace(input, dictionary);

                // Assert
                Assert.AreEqual("temporary", result);
            }

            [TestMethod]
            public void Replace_WithMultipleKeysAndValuesInDictionary_ReturnsReplacedString()
            {
                // Arrange
                string input = "$temp$ here comes the name $name$";
                var dictionary = new Dictionary<string, string> { { "temp", "temporary" }, { "name", "John Doe" } };

                // Act
                string result = DictionaryReplacer.Replace(input, dictionary);

                // Assert
                Assert.AreEqual("temporary here comes the name John Doe", result);
            }
        }
    

}
