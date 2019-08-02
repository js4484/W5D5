

bsearch
array, target, returns idx, sorted array, recursive

def bsearch(arr, target)
    return nil if arr.empty?
    midpoint = arr.length / 2
    #0
    return midpoint if arr[midpoint] == target
    #-1
    if target < arr[midpoint] 
        return bsearch(arr[0...midpoint], target)
    #1
    elsif target > arr[midpoint] 
        return output = midpoint + bsearch(arr[(midpoint+1)..-1], target)
    end
end


my_flatten to specified level; default to return nested


class Array
    def my_flatten(ele = nil)
        arr = self.dup
        return arr if ele == 0
        if 
        
            next_level = ele - 1
        else
            next_level = nil
        end
        arr.each_with_index do |ele, i|
            arr[i] = my_flatten(next_level) if ele.is_a?(Array)
        end
        
        arr
    end
end

[["a"], "b", ["c", "d", ["e"]]].my_flatten(1) = ["a", "b", "c", "d", ["e"]]

[1, 2, [3, 4]] ==> [1, 2, 3, 4]

[1, 2, [3, [4]]] ==> [1, 2, 3, [4]]



myreduce, array meth, block on each el, combine each result, one by one, with given accumulator, if no acc, first el is used

### my_reduce

Write an array method that calls the given block on each element and
combines each result one-by-one with a given accumulator. If no accumulator is given, the first element is used.


class Array
  def my_reduce(accumulator = nil, &block)
    i = 0
    if accumulator.nil?
      accumulator = self.first
      i += 1
    end

    while i < length
      accumulator = block.call(accumulator, self[i])
      i += 1
    end
    accumulator
  end
end

block.call(accumulator, self[i])


class Array
    def my_reduce(accumulator = nil, &block)
        arr = self.dup
        if accumulator?
            arr.each do |ele|
                accumulator = block.call(accumulator, ele)
            end
        else
            accumulator = arr.shift
            arr.each do |ele|
                accumulator =block.call(accumulator, ele)
            end
        end
        accumulator
    end
end
